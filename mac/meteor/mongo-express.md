https://github.com/andzdroid/mongo-express

换成 mongo-express 单独运行，不与 meteor 混在一起

安装 mongo-express，在用户主目录下，新建一个文件夹 mongo-express

    cd mongo-express
    npm install mongo-express

安装完之后，进入 node_modules 目录下，复制文件 config.default.js 为 config.js

    cp config.default.js config.js

修改 config.js 文件，把 mongodb 的 port 端口号设置为 3001

    mongodb: {
      server: 'localhost',
      port: 3001,

端口号可以通过在 meteor 项目中启动 meteor mongo 命令得到。

修改 config.js 中的另一个地方：

    //readOnly: if readOnly is true, components of writing are not visible.
    readOnly: false

然后运行 mongo-express，在 mongo-express 目录下执行命令：

    node app

在浏览器中，访问 localhos:8081 地址，这时需要用户认证，

    basicAuth: {
      username: 'admin',
      password: 'pass'
    },

上面的用户名和密码来自配置文件 config.js，输入上面的用户名和密码，就能访问 mongodb 数据库中存储的信息了

注意： 启动 mongo-express 的时候，meteor 项目是运行着的
