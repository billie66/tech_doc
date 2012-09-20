ubuntu server 11.04

* Append the below line to the end of the file /etc/apt/sources.list
    
    deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen

* Update package

    sudo apt-get update

* Add GPG key

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10

* Install mongodb-10gen

    sudo apt-get install mongodb-10gen

* Post-Installation

Now, MongoDB is installed, started, and auto start MongoDB script is
generated to `/etc/init/mongo` and `/etc/init.d/mongo`. In addition, all
MongoDB files are copied to `/usr/bin` folder.

The main configuration file `mongodb.conf` is located at `/etc/mongodb.conf`, 
change the values to customize your mongoDB server.

* Verification

To verify it, just connect it with “mongo”

<http://www.mkyong.com/mongodb/how-to-install-mongodb-on-ubuntu/>

