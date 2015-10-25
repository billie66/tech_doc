https://www.digitalocean.com/community/tutorials/how-to-deploy-a-meteor-js-application-on-ubuntu-14-04-with-nginx

部署到阿里云服务器

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
cd bundle
export MONGO_URL=mongodb://localhost:27017/meteor
export ROOT_URL=http://meteor.haoduoshipin.com
export PORT=8000
node main.js
```

start application with the command `node main.js`, print the following error messages:

>Error: /home/peter/meteor/bundle/programs/server/npm/npm-bcrypt/node_modules/bcrypt/build/Release/bcrypt_lib.node: invalid ELF header

The bcrypt module compiled on mac does not work on linux, so the solution is to reinstall bcrypt on linux

```bash
cd /home/peter/meteor/bundle/programs/server/npm/npm-bcrypt/node_modules/
npm install bcrypt
```

* configuring Upstart

create a new file named /etc/init/meteor.conf filling with the content below, you should use root status

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

then check the syntax of file `/etc/init/meteor.conf`, with the command:

```
init-checkconf /etc/init/meteor.conf
```

if there are not syntax errors, the output of this command is:

>File /etc/init/testjob.conf: syntax ok

start the Upstart jobs

```
sudo service meteor start
```

then your application will run in the background
