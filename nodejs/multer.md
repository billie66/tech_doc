在 Express.js 框架中借助 multer
中间件上传文件，配置 multer 的上传路径 `dest` 的时候，若使用的是相对路径，那么相对路径的参考点是当启动项目的时候，你执行命令 `node blah.js` 所在的目录。 这里的 `blah.js` 代指的是项目的启动文件名称。如下所示：

```
var upload = multer({dest: 'public/uploads'});
```

服务器上通过 pm2 来管理 Node.js 项目，若在项目目录之外，比方说在服务器的主目录下启动项目，运行下面命令，其中 `xxx` 代表项目名称：

```
pm2 start xxx/blah.js
```

这样启动项目的话，multer 就会把主目录当做文件上传路径的参考点，把上传的文件存放到 `~/public/uploads` 目录下，所以在配置 multer 上传文件的路径的时候应该使用绝对路径。

```
var path = require('path');
var multer = require('multer');
var upload = multer({dest: path.join(__dirname, 'public/uploads')});
```
