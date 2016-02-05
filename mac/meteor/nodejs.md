### 使用 nodejs 的接口

```
var fs = Npm.require('fs');
var path = Npm.require('path');
__ROOT_APP_PATH__ = fs.realpathSync('.');
console.log(__ROOT_APP_PATH__);
console.log(process.env.PWD);
console.log(path.join(process.env.PWD, '../data'));
if (!fs.existsSync('/Users/peter/meteor/data/posts.json')) {
    throw new Error(" does not exists");
}
```


### 从 meteor 项目之外读取硬盘文件

http://stackoverflow.com/questions/28105957/meteor-and-the-private-directory
