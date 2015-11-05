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
ls
```

meteor 目录包含如下文件：

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

然后，回到应用的根目录 ~/meteor，导出一些环境变量：

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
    exec node /home/meteor/bundle/main.js >> /home/meteor/meteor.log
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
restart meteor
```
