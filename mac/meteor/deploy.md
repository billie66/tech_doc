参考文档：

https://www.digitalocean.com/community/tutorials/how-to-deploy-a-meteor-js-application-on-ubuntu-14-04-with-nginx

### 部署到阿里云服务器

* 系统已经安装了 nodejs 和 nginx，并且 meteor.haoduoshipin.com 已经能够访问

* 安装 mongodb 成功


* build meteor app on local machine

```
cd ~/meteor/haoduoshipin
meteor build .
```

this will generate a tarball named haoduoshipin.tar.gz, then copy the tarball to the remote server:

```
scp haoduoshipin.tar.gz hostname:~/meteor
```

* login to server with ssh

```
cd meteor
tar -zxf haoduoshipin.tar.gz
```

meteor/bundle 目录包含如下文件：

```
main.js  programs  README  server  star.json
```

其中 README 文件内容：

```
This is a Meteor application bundle. It has only one external dependency:
Node.js 0.10.40 or newer. To run the application:

  $ (cd programs/server && npm install)
  $ export MONGO_URL='mongodb://user:password@host:port/databasename'
  $ export ROOT_URL='http://example.com'
  $ export MAIL_URL='smtp://user:password@mailhost:port/'
  $ node main.js

Use the PORT environment variable to set the port where the
application will listen. The default is 80, but that will require
root on most systems.

Find out more about Meteor at meteor.com.
```

下面就根据 README 文件中的步骤操作, 首先按照 NPM 模块：

```
cd programs/server && npm install
```

然后，回到应用的根目录 ~/meteor/bundle，导出一些环境变量：

```
export MONGO_URL=mongodb://localhost:27017/meteor
export ROOT_URL=http://meteor.haoduoshipin.com
export PORT=8000
```

最后启动应用：

```
node main.js
```

### 遇到的问题

启动应用 `node main.js`, 一般会打印出如下错误信息：

>Error: /home/peter/meteor/bundle/programs/server/npm/npm-bcrypt/node_modules/bcrypt/build/Release/bcrypt_lib.node: invalid ELF header

这是因为在 mac 上编译的 bcrypt 模块，不能在 Linux 系统上工作，所以需要在 Linux 系统上重新安装 bcrypt 模块：

```bash
cd ~/meteor/bundle/programs/server/npm/npm-bcrypt/node_modules/
npm install bcrypt
```

### 配置 Upstart

手动运行 `node main.js` Meteor 应用运行在前台，当退出登录之后，应用就终止了。那如何让应用始终运行呢，可以配置 Upstart

1. create a new file named /etc/init/meteor.conf filling with the content below, you should use root status

```
# upstart service file at /etc/init/meteor.conf
description "Meteor.js (NodeJS) application"
author "Billie Zhang <billiecoder@gmail.com>"

# When to start the service
start on started mongodb and runlevel [2345]

# When to stop the service
stop on shutdown

# Automatically restart process if crashed
respawn
respawn limit 10 5

# we don't use buil-in log because we use a script below
# console log

# drop root proviliges and switch to mymetorapp user
#setuid todos
#setgid todos

script
    export PATH=/opt/local/bin:/opt/local/sbin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    export NODE_PATH=/usr/lib/nodejs:/usr/lib/node_modules:/usr/share/javascript
    # set to home directory of the user Meteor will be running as
    export PWD=/home/peteor/meteor
    export HOME=/home/peteor/meteor
    # leave as 127.0.0.1 for security
    export BIND_IP=127.0.0.1
    # the port nginx is proxying requests to
    export PORT=8000
    # this allows Meteor to figure out correct IP address of visitors
    export HTTP_FORWARDED_COUNT=1
    # MongoDB connection string using meteor as database name
    export MONGO_URL=mongodb://localhost:27017/meteor
    # The domain name as configured previously as server_name in nginx
    export ROOT_URL=http://meteor.haoduoshipin.com
    # optional JSON config - the contents of file specified by passing "--settings" parameter to meteor command in development mode
    #export METEOR_SETTINGS='{ "somesetting": "someval", "public": { "othersetting": "anothervalue" } }'
    # this is optional: http://docs.meteor.com/#email
    # commented out will default to no email being sent
    # you must register with MailGun to have a username and password there
    # export MAIL_URL=smtp://postmaster@mymetorapp.net:password123@smtp.mailgun.org
    # alternatively install "apt-get install default-mta" and uncomment:
    # export MAIL_URL=smtp://localhost
    exec node /home/peter/meteor/bundle/main.js >> /home/peter/meteor/meteor.log
end script
```

2. then check the syntax of file `/etc/init/meteor.conf`, with the command:

```
init-checkconf /etc/init/meteor.conf
```

if there are not syntax errors, the output of this command is:

>File /etc/init/testjob.conf: syntax ok

3. start the Upstart jobs

```
sudo service meteor start
```

4. check if the meteor service is running

```
status meteor
```

5. restart the meteor service

```
sudo service meteor restart
```

这样，Meteor 应用就始终在后台运行了。

### 再次部署

第一次部署成功之后，再部署就轻车熟路了，重复下面的操作

* 本地开发机器

```
meteor build .
scp appname.tar.gz hostname.com:~/appname
```

* 远端服务器

```
cd ~/appname
tar -zxf appname.tar.gz
cd bundle/programs/server
npm install
cd npm/npm-bcrypt/node_modules/
npm install bcrypt
sudo service meteor restart
```

## 在同一台服务器部署一个新的项目

解压 meteor 的 tarball 后，安装 npm 模块，得到错误信息

```
make: *** [Release/obj.target/fibers/src/fibers.o] Error 1
make: Leaving directory `/home/peter/chat/bundle/programs/server/node_modules/fibers/build'
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/home/peter/.nvm/versions/node/v5.3.0/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:270:23)
gyp ERR! stack     at emitTwo (events.js:87:13)
gyp ERR! stack     at ChildProcess.emit (events.js:172:7)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:200:12)
gyp ERR! System Linux 3.13.0-32-generic
gyp ERR! command "/home/peter/.nvm/versions/node/v5.3.0/bin/node" "/home/peter/.nvm/versions/node/v5.3.0/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild" "--release"
gyp ERR! cwd /home/peter/chat/bundle/programs/server/node_modules/fibers
gyp ERR! node -v v5.3.0
gyp ERR! node-gyp -v v3.0.3
gyp ERR! not ok
Build failed
```

需要安装 node v0.10.40 才能编译 fiber，参考官方文档 http://guide.meteor.com/deployment.html#custom-deployment

```
server@aliyun:~/pet$ nvm ls
->     v0.10.40
         v4.1.1
         v5.3.0
         system
default -> 5.3.0 (-> v5.3.0)
node -> stable (-> v5.3.0) (default)
stable -> 5.3 (-> v5.3.0) (default)
iojs -> N/A (default)
```

### 导出端口

因为已经有一个 meteor 项目在监听 8000 端口，所以新的 meteor 项目需要不同的端口

```
server@aliyun:~/pet$ node main.js

events.js:72
        throw er; // Unhandled 'error' event
              ^
Error: listen EADDRINUSE
    at errnoException (net.js:905:11)
    at Server._listen2 (net.js:1043:14)
    at listen (net.js:1065:10)
    at net.js:1147:9
    at dns.js:72:18
    at process._tickCallback (node.js:448:13)
```

解决办法

```
export PORT=9000
```

### 配置一个域名

到 /etc/nginx/sites-enabled 目录下, 新建一个文件名为 chat.conf

```
server {
    listen         80;
  server_name chat.haoduoshipin.com;

    location / {
        proxy_pass http://localhost:9000;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $http_x_forwarded_host;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_read_timeout 3m;
        proxy_send_timeout 3m;
    }
}
```

别忘了，重新启动 nginx

```
sudo service nginx reload
```

### 配置一个 upstart service

到 /etc/init/ 目录下，新建一个文件 chat.conf，文件内容如下：

```
# upstart service file at /etc/init/todos.conf
description "Meteor.js (NodeJS) application"

# When to start the service
start on started mongodb and runlevel [2345]

# When to stop the service
stop on shutdown

# Automatically restart process if crashed
respawn
respawn limit 10 5

script
    export PATH=/opt/local/bin:/opt/local/sbin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    export NODE_PATH=/usr/lib/nodejs:/usr/lib/node_modules:/usr/share/javascript
    # set to home directory of the user Meteor will be running as
    export PWD=/home/peter/chat
    export HOME=/home/peter/chat
    # leave as 127.0.0.1 for security
    export BIND_IP=127.0.0.1
    # the port nginx is proxying requests to
    export PORT=9000
    # this allows Meteor to figure out correct IP address of visitors
    export HTTP_FORWARDED_COUNT=1
    # MongoDB connection string using todos as database name
    export MONGO_URL=mongodb://localhost:27017/meteor
    # The domain name as configured previously as server_name in nginx
    export ROOT_URL=https://chat.haoduoshipin.com
    exec node /home/peter/chat/bundle/main.js >> /home/peter/chat/chat.log
end script
```

然后在命令行中运行：

```
sudo service chat start
```

### how to determine which node version meteor is running on

到 meteor 的项目目录下 .meteor/local/build 下，有一个文件 .node_version.txt，写明了 meteor 所用的 Node 版本

```
$ cd .meteor/local/build
$ cat .node_version.txt
v0.10.40
```

### reference

* https://github.com/meteor/meteor/issues/5124
* https://forums.meteor.com/t/meteor-nodejs-0-12/2769
* https://meteorhacks.com/how-meteor-uses-node.html
