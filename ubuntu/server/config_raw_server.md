系统 Ubuntu 16.04

### install nginx

```
sudo apt-get install nginx
```

添加的域名配置文件

到 /etc/nginx/sites-available/ 目录配置域名

```
server {
    listen     80 default_server;
    server_name 128.199.119.191;

    location / {
        proxy_pass http://localhost:8000;
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

测试添加的域名配置文件是否正确

```
nginx -t -c /etc/nginx/nginx.conf
```

参考 https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04

重新启动 nginx

```
sudo systemctl restart nginx
```

查看 nginx 运行状态

```
systemctl status nginx
```

### install mongodb 3.2

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

上述步骤安装好 Mongodb 之后，启动 mongodb 之前，需要运行下面命令，要不然 mongodb 启动不起来

```
sudo rm /var/lib/mongodb/mongod.lock
sudo mongod --repair
```

参考 http://stackoverflow.com/questions/24899849/connection-refused-to-mongodb-errno-111

然后，启动 mongodb

```
sudo vim /etc/systemd/system/mongodb.service
sudo systemctl start mongodb
sudo systemctl status mongodb
```

新创建的 `/etc/systemd/system/mongodb.service` 文件内容

```
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target

[Service]
User=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target
```

Digital Ocean [how-to-install-mongodb-on-ubuntu-16-04](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04)

### install NVM

```
sudo apt-get update
sudo apt-get install build-essential libssl-dev
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh -o install_nvm.sh
bash install_nvm.sh
source ~/.bashrc
```

<https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04>

### install Node.js

```
nvm install 6.3.1
nvm alias default 6.3.1
```

