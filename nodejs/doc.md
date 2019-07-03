### session-cookie
https://medium.com/@evangow/server-authentication-basics-express-sessions-passport-and-curl-359b7456003d

### install nvm on ubuntu 16.04

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
source .bashrc
```

### install nodejs

```
nvm install v10.15.2
```

### install mongodb

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

### install yarn

```
npm install -g yarn
```

### install pm2

```
npm install -g pm2
```

### install nginx

```
sudo apt-get install nginx
```


```
server {
    listen       80;
    server_name  patent.maodou.io:3006;

    location / {
        proxy_pass http://localhost:3006;
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

