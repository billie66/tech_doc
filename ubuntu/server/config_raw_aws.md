Ubuntu LTS 14.04 server

### install nvm

```
sudo apt-get update
sudo apt-get install build-essential libssl-dev
```

```
curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh
source .bashrc
```

```
nvm ls-remote
```

### install nodejs

```
nvm install 6.3.1
nvm alias default 6.3.1
```

```
ubuntu@ip-172-31-18-114:~$ node -v
v6.3.1
ubuntu@ip-172-31-18-114:~$ npm -v
3.10.3
ubuntu@ip-172-31-18-114:~$
```

### install git

```
sudo apt-get install git
```

### install mongodb 3.2

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```


```
ubuntu@ip-172-31-18-114:~$ service mongod status
mongod stop/waiting
```

<https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/>

### install nginx

```
sudo apt-get update
sudo apt-get install nginx
```

```
ubuntu@ip-172-31-18-114:~$ service nginx status
 * nginx is running
```

