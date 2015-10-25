### Install mongodb on ubuntu server 14.04

The tutorial is from https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

* Import the public key used by the package management system.

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

* Create a list file for MongoDB. (ubuntu 14.04)

    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list

* Reload local package database.

    sudo apt-get update

* Install the latest stable version of MongoDB.

    sudo apt-get install -y mongodb-org

* Start MongoDB

    sudo service mongod start

* Verify that MongoDB has started successfully

    ps aux | grep mongod

* Stop MongoDB

    sudo service mongod stop

* Restart MongoDB

    sudo service mongod restart

* Remove Packages

    sudo apt-get purge mongodb-org*

* Remove Data Directories

    sudo rm -r /var/log/mongodb
    sudo rm -r /var/lib/mongodb

The following document comes from [here](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-meteor-js-application-on-ubuntu-14-04-with-nginx)

To be sure that access from external hosts is not possible, we execute the following to be sure that MongoDB is bound to 127.0.0.1. Check with this command:

    netstat -ln | grep -E '27017|28017'

Expected output:

    tcp        0      0 127.0.0.1:27017         0.0.0.0:*               LISTEN
    tcp        0      0 127.0.0.1:28017         0.0.0.0:*               LISTEN
    unix  2      [ ACC ]     STREAM     LISTENING     6091441  /tmp/mongodb-27017.sock

In order to have daily backups available in case something goes wrong, we can optionally install a simple command as a daily cron job. Create a file /etc/cron.d/mongodb-backup:

    @daily root mkdir -p /var/backups/mongodb; mongodump --db todos --out /var/backups/mongodb/$(date +'\%Y-\%m-\%d')
