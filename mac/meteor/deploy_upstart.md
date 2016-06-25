# 部署项目到服务器

依赖工具：

* Ubuntu 14.04.1 LTS (GNU/Linux 3.13.0-32-generic x86_64)
* nginx v1.6.2
* mongodb-org v3.0
* nodejs
* 服务器 aliyun

到目前为止，这个基于 meteor 的聊天室小应用已经开发完成了，接下来要做的工作就是把它部署到服务器上。

### 本地准备工作

在部署之前，我们还需要在本地做些工作，来到我们的项目根目录中，执行命令：

```
cd meteor-react-bird-demo
meteor remove insecure
```

执行上面的命令之后，我们删除了一个叫做 insecure 的软件包。这个软件包是 meteor
默认安装的，它的作用是允许客户端代码可以直接修改数据库中的数据。在项目中我们创建了一个叫做 `Messages` 的 mongodb collection，因为 insecure 软件包的存在，其实我们可以在客户端代码中直接调用 `Messages.insert()` 接口把聊天内容插入到数据库中，在生产环境下会引发安全问题。

另外一个工作就是把项目代码打包成一个 tarball，执行命令：

```
cd meteor-react-bird-demo
npm install --production
meteor build ../build --architecture os.linux.x86_64
```

在运行打包命令 [meteor build](http://docs.meteor.com/#/full/meteorbuild) 之前
命令执行完之后，会在 `../build` 目录下生成一个名为 meteor-react-bird-demo.tar.gz 的 tarball。请参考

然后把 meteor-react-bird-demo.tar.gz 软件包传送到服务器上的 home 主目录下，运行命令：

```
scp meteor-react-bird-demo.tar.gz your_name@your_domain_name:~/
```

当然在具体操作的时候，需要把 `your_name` 和 `your_domain_name` 替换为您自己的用户名和域名。

到目前为止，本地开发机上的工作就全部完成了，后续工作全部在服务器上完成。

### 服务器上的准备工作

首先要登录到远端服务器，执行命令：

```
ssh your_name@your_domain_name
```

登录成功之后，在服务器的 home 主目录下，新创建一个名为 chat 的目录，把从本地传送过来的 meteor-react-bird-demo.tar.gz 移到 chat 目录中待用：

```
mkdir chat
cp ../s3-meteor.tar.gz .
```

#### 设置 Nginx web 服务器

如果服务器上没有 Nginx，首先安装 Nginx

```
sudo apt-get install nginx
```

配置一个域名，到 `/etc/nginx/sites-enabled` 目录下, 新建一个文件名为 chat.conf

```
cd /etc/nginx/sites-enabled
sudo touch chat.conf
```

`/etc/nginx/sites-enabled/chat.conf` 文件中的内容如下：

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

上面的配置文件，其中 `server_name` 需要用你自己的域名代替，这里就用 `chat.haoduoshipin.com` 为例说明。另外，`http://localhost:9000` 代码中的`9000`是端口号，要确保没有被其它应用占用，若被占用了，则修改为其它空闲端口号，如 3001 端口。

然后在命令行中运行命令，重新启动 Nginx：

```
sudo service nginx reload
```

* 如何为网站绑定域名， 可以参考[好多视频的第131期](http://haoduoshipin.com/v/131)
* 如何配置 nginx，可以参考[好多视频的第130期](http://haoduoshipin.com/v/130)
* 如何申请服务器，可以参考[好多视频的第129期](http://haoduoshipin.com/v/129)

#### 安装 mongodb 数据库

在本地开发 meteor 项目的时候，不需要单独安装 mongodb 数据库，不过把项目部署到服务器上，则需要我们手动安装 mongodb 数据库。

安装步骤按照 mongodb 官方提供的文档，[Ubuntu v14.04 中安装 mongodb 3.0](https://docs.mongodb.org/v3.0/tutorial/install-mongodb-on-ubuntu/)

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

安装成功之后，执行命令 `mongo`，

```
server@aliyun:~$ mongo
MongoDB shell version: 3.0.7
connecting to: test
Server has startup warnings:
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten]
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/enabled is 'always'.
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten]
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/defrag is 'always'.
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2015-10-25T15:53:28.875+0800 I CONTROL  [initandlisten]
>
```

命令执行结果有两条警告信息打印出来，如何消除这些警告信息呢，可以参考[官方文档](https://docs.mongodb.org/manual/tutorial/transparent-huge-pages/#transparent-huge-pages-thp-settings)，也可以按照下面的方法解决：

到 /etc/init 目录下，修改 mongodb 的配置文件 mongod.conf

```
server@aliyun:/etc/init$ sudo vim mongod.conf
```

打开 /etc/init/mongod.conf 文件之后，添加下面一些代码，新添加的代码位于中文注释之间：

```
  chown $DAEMONUSER /var/run/mongodb.pid
  # 新添加的代码开始位置
  if test -f /sys/kernel/mm/transparent_hugepage/enabled; then
    echo never > /sys/kernel/mm/transparent_hugepage/enabled
  fi
  if test -f /sys/kernel/mm/transparent_hugepage/defrag; then
    echo never > /sys/kernel/mm/transparent_hugepage/defrag
  fi
  # 新添加的代码结束位置
end script
```

然后保存文件，重新启动 mongod 服务

```
server@aliyun:/etc/init$ sudo service mongod restart
```

这时再次运行 mongo 命令，就不会出现警告信息了。

```
server@aliyun:/etc/init$ mongo
MongoDB shell version: 3.0.7
connecting to: test
>
```

注意：目前 mongodb 官方最新版本是 v3.2，[参考文档](https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/)

#### 安装 nodejs

Meteor 是基于 nodejs 的框架，并且 meteor 安装包自带了 nodejs 环境，所以开发 meteor 应用的时候，我们不需要手动安装 nodejs，就能把应用跑起来。但是部署 meteor 应用的时候，情形就不一样了。我们需要手动安装 nodejs，可是 nodejs 版本众多，到底安装哪一个版本呢？

从 meteor v1.2 版的官方部署文档，[自定义部署](http://guide.meteor.com/deployment.html#custom-deployment)部分得知，meteor 是运行在 nodejs v0.10.x 之上的，具体的 nodejs 版本号可以这样得到，到本地 meteor 项目目录 `.meteor/local/build` 下，有一个隐藏文件 `.node_version.txt`，写明了 meteor 所用的 Node 版本

```
$ meteor --version
Meteor 1.2.1
$ cd .meteor/local/build
$ cat .node_version.txt
v0.10.40
```

所以在服务器上，我们需要安装 nodejs-v0.10.40 版本，到服务器的命令行中运行：

```
nvm install v0.10.40
```

#### 安装 npm 模块并运行项目

回到服务器的 ~/chat 目录下，解压 s3-meteor.tar.gz 软件包：

```
server@aliyun:~/chat$ tar -zxf haoduoshipin.tar.gz
```

解压之后，查看一下 `~/chat` 目录下的文件，运行 `ls` 命令，输出结果：

```
server@aliyun:~/chat$ ls
bundle  s3-meteor.tar.gz
```

进入到 `~/chat/bundle` 目录下，运行 `ls` 命令，输出结果：

```
server@aliyun:~/chat/bundle$ ls
main.js  programs  README  server  star.json
```

上面列出的 README 文件内容如下：

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

下面就根据 README 文件中的步骤进行操作, 首先安装 npm 模块，进入到 `~/chat/bundle/programs/server` 目录下

```
server@aliyun:~/chat/bundle$ cd programs/server
server@aliyun:~/chat/bundle/programs/server$ ls
app                 boot.js             npm                 packages
assets              config.json         npm-shrinkwrap.json program.json
boot-utils.js       mini-files.js       package.json        shell-server.js
```

在安装 npm 模块之前，我们需要检查一下当前运行的 nodejs 版本：

```
server@aliyun:~/chat/bundle/programs/server$ nvm ls
       v0.10.40
         v4.1.1
->       v5.3.0
         system
default -> 5.3.0 (-> v5.3.0)
node -> stable (-> v5.3.0) (default)
stable -> 5.3 (-> v5.3.0) (default)
iojs -> N/A (default)
```

从上面的输出结果中可以看出，服务器上当前运行的 nodejs 版本是 v5.3.0，而不是 v0.10.40。之前我们已经知道了，meteor 1.2.1 依托的 nodejs 版本是 v0.10.40，所以我们要改变当前运行的 nodejs 版本，要不然应用所需要的 npm 模块是不能编译成功的，执行命令：

```
server@aliyun:~/chat/bundle/programs/server$ nvm use v0.10.40
->     v0.10.40
         v4.1.1
         v5.3.0
         system
default -> 5.3.0 (-> v5.3.0)
node -> stable (-> v5.3.0) (default)
stable -> 5.3 (-> v5.3.0) (default)
iojs -> N/A (default)
```

nodejs 环境设置好之后，就能顺利安装 npm 模块了：

```
server@aliyun:~/chat/bundle/programs/server$ npm install
```

npm 模块都装好之后，回到项目根目录 `~/chat/bundle`，导出几个环境变量。首先导出项目所需要的 mongodb 数据库的地址：

```
server@aliyun:~/chat/bundle$ export MONGO_URL=mongodb://localhost:27017/chat
```

上面命令中的 `chat` 是创建的 mongodb 数据库的名字，如果在命令行中执行下面命令，可以直接访问 `chat` 数据库：

```
server@aliyun:~/chat/bundle$ mongo localhost:27017/chat
``

然后是导出项目域名地址和可访问的端口，这些都是在 nginx 配置文件中设置好的：

```
server@aliyun:~/chat/bundle$ export ROOT_URL=http://chat.haoduoshipin.com
server@aliyun:~/chat/bundle$ export PORT=9000
```

注意这里的端口号要与 nginx 配置文件 chat.conf 中使用的端口号保持一致。当所有的设置都完成之后，我们就可以启动应用了，执行下面的命令：

```
server@aliyun:~/chat/bundle$ node main.js
```

但不幸的是，应用并不能成功运行起来，一般会报告如下错误信息：

>Error: /home/your_name/chat/bundle/programs/server/npm/npm-bcrypt/node_modules/bcrypt/build/Release/bcrypt_lib.node: invalid ELF header

这是因为在 mac 上编译的 bcrypt 模块，不能在 Linux 系统上工作，所以需要在 Linux 系统上重新安装 bcrypt 模块，注意 nodejs 版本为 v0.10.40

```
server@aliyun:~/chat/bundle$ cd programs/server/npm/npm-bcrypt/node_modules/
server@aliyun:~/chat/bundle/programs/server/npm/npm-bcrypt/node_modules$ npm install bcrypt
```

重新安装 bcrypt 模块之后，回到项目根目录：

```
server@aliyun:~/chat/bundle$ node main.js
```

这时，项目就成功运行起来了，打开浏览器，访问地址 `http://chat.haoduoshipin.com`，就可以看到项目主页了。


### 配置 upstart 任务

手动运行 `node main.js` 虽然可以启动应用，但是当您从服务器退出登录之后，应用就终止运行了。那如何让应用始终运行呢，可以配置 Upstart 服务

首先进入到 /etc/init/ 目录下面，创建一个文件 chat.conf，当然需要 root 身份

```
cd /etc/init/
sudo vim chat.conf
```

打开 `/etc/init/chat.conf` 文件之后，粘贴如下内容并保存，其中以 # 开头的语句是注释：

```
# upstart service file at /etc/init/chat.conf

# When to start the service
start on started mongodb and runlevel [2345]

# When to stop the service
stop on shutdown

# Automatically restart process if crashed
respawn
respawn limit 10 5

script
    export PATH=/home/peter/.nvm/versions/node/v5.4.1/bin:/opt/local/bin:/opt/local/sbin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

    # set to home directory of the user Meteor will be running as
    export PWD=/home/peter
    export HOME=/home/peter
    # leave as 127.0.0.1 for security
    export BIND_IP=127.0.0.1
    # the port nginx is proxying requests to
    export PORT=3000
    # this allows Meteor to figure out correct IP address of visitors
    export HTTP_FORWARDED_COUNT=1
    # MongoDB connection string using meteor as database name
    export MONGO_URL=mongodb://localhost:27017/haoqicat
    # The domain name as configured previously as server_name in nginx
    export ROOT_URL=http://haoqicat.com
    exec node /home/peter/secondstep/bundle/main.js >> /home/your_name/chat/chat.log
end script
```

检查文件 `/etc/init/meteor.conf` 语法是否正确，不需要 root 身份，运行命令：

```
init-checkconf /etc/init/chat.conf
```

如果没有语法错误，输出结果为：

>File /etc/init/testjob.conf: syntax ok

启动新创建的 chat upstart 服务

```
sudo service chat start
```

这样，Meteor 应用就始终在后台运行了。


### 参考文档

* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-meteor-js-application-on-ubuntu-14-04-with-nginx

* https://www.digitalocean.com/community/tutorials/the-upstart-event-system-what-it-is-and-how-to-use-it
