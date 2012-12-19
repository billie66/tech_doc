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
generated to `/etc/init/mongodb.conf` and `/etc/init.d/mongodb`. In addition, all
MongoDB files are copied to `/usr/bin` folder.

The main configuration file `mongodb.conf` is located at `/etc/mongodb.conf`, 
change the values to customize your mongoDB server.

* Verification

To verify it, just connect it with “mongo”

<http://www.mkyong.com/mongodb/how-to-install-mongodb-on-ubuntu/>

Once MongoDB is installed and configured you can visit http://localhost:28017/
to see if it’s working.

### check mongodb on or off

* chkconfig mongodb

### rails & mongodb

* bundle
* sudo apt-get install advancecomp  //for installing advpng
* mongod &
* rake db:drop
* rake db:seed
* upload an app

* install java, google `webupd8 java ppa`, then click the first item

  sudo add-apt-repository ppa:webupd8team/java
  sudo apt-get update
  sudo apt-get install oracle-java7-installer

* go to vendor/solr/sunspot_solr_mmseg4j, run the command below

  java -jar start.jar

### rails

* rails g scaffold micro_video title:string url:text
