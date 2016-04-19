ubuntu 14.04

### install nginx and config nginx

```
sudo apt-get install nginx
```

go to `/etc/nginx/site-enabled` directory, delete `default` file, then create a new file `app.conf`

```
server {
    listen         80;
    server_name your_server_name;

    location / {
        proxy_pass http://localhost:3000;
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

then run command `sudo service nginx restart`

### install git

```
sudo apt-get install git
```

### install nvm

```
sudo apt-get install curl
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
source .bashrc
```

### install nodejs

```
nvm install iojs-v3.3.1
```

add the following code snippet to the end of .bashrc file

```
alias cnpm="npm --registry=https://registry.npm.taobao.org \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npm.taobao.org/dist \
  --userconfig=$HOME/.cnpmrc"
```

then run command `source .bashrc` in the command line.

### install meteor

```
curl https://install.meteor.com/ | sh
```

### run meteor app

```
cd myapp
npm install
meteor
```

### install mongodb (v3.0)

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

reference <https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/>

