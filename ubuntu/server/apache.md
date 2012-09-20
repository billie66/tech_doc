### install apache 

    sudo apt-get install apache2

### apache config file

    echo SeverName www.book.org:80 >/etc/apache2/httpd.conf

### available site

    <VirtualHost *:80>
        ServerAdmin webmaster@book.org
        ServerName book.org
        DocumentRoot /home/billie/book/public
        RailsEnv development
        <Directory /home/billie/book/public>
            AllowOverride all
            Options -MultiViews
        </Directory>
    <VirtualHost>

[good site][http://library.linode.com/lamp-guides/ubuntu-11.04-natty#sph_install-and-configure-the-apache-web-server]



