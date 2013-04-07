### Install mongodb on ubuntu

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

* Lauch mongodb server

    --- On ubuntu 12.04 ---
    rm /var/lib/mongodb/mongod.lock ( can't run two deamon simultaneously)
    sudo service mongodb start
    --- end ---

* Lauch mongodb server

    --- On ubuntu 11.04 ---
    mkdir /data/db/
    mkdir /data/db/journal
    rm  /data/db/mongod.lock
    mongod &
    --- end ---

* Verification

To verify it, just connect it with “mongo”

<http://www.mkyong.com/mongodb/how-to-install-mongodb-on-ubuntu/>

Once MongoDB is installed and configured you can visit http://localhost:28017/
to see if it’s working.

### check mongodb on or off

* chkconfig mongodb

### rails & mongodb (for vplayer.net)

* why install memcashed in development env?(for cache all assets files)

Since the setting in the file config/environment/development.rb:

  config.action_controller.perform_caching = true

so if change the value from `true` to `false`, then the assets will not be cached.

* sudo apt-get insatll libxml2-dev libxslt-dev (for nokogiri)
* sudo apt-get install -y advancecomp gifsicle jpegoptim libjpeg-progs optipng pngcrush (for image_optim)
* sudo apt-get install imagemagick (for uploading images)
* bundle install
* sudo service mongodb start
* rake db:drop
* rake db:seed
* upload an app

* install java, google `webupd8 java ppa`, then click the first item

  sudo add-apt-repository ppa:webupd8team/java
  sudo apt-get update
  sudo apt-get install oracle-java7-installer

* go to vendor/solr/sunspot_solr_mmseg4j, run the command below

  java -jar start.jar

### tips

* reference && embedded association

    When you’re deciding which of these approaches is to use you need to ask
    yourself if you’ll ever need the associated records to stand on their own
    or if you’ll always be accessing them through their parent model. 

* User.skip(2).first

* show dbs

* use dbname

* show collections

* db.blogs.find()

* db.blogs.help()

* db.help()
