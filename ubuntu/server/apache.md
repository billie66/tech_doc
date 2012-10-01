### install apache 

    sudo apt-get install apache2

### apache config file

    echo SeverName www.book.org:80 >/etc/apache2/httpd.conf

### create a virtual host 

    <VirtualHost *:80>
        ServerAdmin webmaster@book.org
        ServerName book.org
        DocumentRoot /home/billie/book/public
        ErrorLog /home/billie/book/public
        CustomLog /home/billie/book/public combined
        RailsEnv development
        <Directory /home/billie/book/public>
            AllowOverride all
            Options -MultiViews
        </Directory>
    <VirtualHost>

### install passenger

    gem install passenger
    rbenv rehash
    passenger-install-apache2-module

### enable the virtual host
    
    sudo a2ensite book.org 
    sudo /etc/init.d/apache2 reload

### disable the virtual host

    sudo a2dissite book.org

[good site][http://library.linode.com/lamp-guides/ubuntu-11.04-natty#sph_install-and-configure-the-apache-web-server]



