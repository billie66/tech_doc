### add a new user

```
sudo adduser billie
```

### add sudo privileges

```
usermod -aG sudo billie
```

check if billie was added to sudo group

```
groups billie
```

the output is `billie : billie sudo`

### install nginx

```
sudo apt-get update
sudo apt-get install nginx
```

### nginx running status

```
systemctl nginx status
```

### check server public IP address

```
sudo apt-get install curl
curl -4 icanhazip.com
```


* https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04
* https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-ubuntu-16-04
