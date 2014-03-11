### install apache

    sudo apt-get install apache2

### install xsendfile module

    sudo apt-get update
    sudo apt-get install libapache2-mod-xsendfile
    sudo a2enmod xsendfile
    sudo service apache2 restart

### in config file

    XSendFile On
    XSendFilePath /apps/application/current/
    XSendFilePath /apps/application/shared/bundle/

### apache config file

    echo ServerName www.book.org:80 >/etc/apache2/httpd.conf

### create a virtual host

    <VirtualHost *:80>
        ServerAdmin webmaster@book
        ServerName book
        DocumentRoot /home/billie/book/public
        ErrorLog /home/billie/book/log/error.log
        CustomLog /home/billie/book/log/access.log combined
        RailsEnv development
        <Directory /home/billie/book/public>
            AllowOverride all
            Options -MultiViews
        </Directory>
    </VirtualHost>

### install passenger

    gem install passenger
    rbenv rehash
    passenger-install-apache2-module

### enable the virtual host

    sudo a2ensite book.org
    sudo /etc/init.d/apache2 reload

### disable the virtual host

    sudo a2dissite book.org

### errors

* Fix: nginx is using the 80 port, so shut down the nginx.

    sudo service apache2 start
    * Starting web server apache2
    (98)Address already in use: make_sock: could not bind to address 0.0.0.0:80
    no listening sockets available, shutting down

* After a new gem installed, you should restart the apache to get the changes.

[good site][http://library.linode.com/lamp-guides/ubuntu-11.04-natty#sph_install-and-configure-the-apache-web-server]

