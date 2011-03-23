mkdir /home/user/public_html
cd  /home/user/public_html
vim index.html

Virtual Hosts(to serve many sites using one ip address)

_Apache2_ has the concept of sites, which are separate configuration files that 
_Apache2_ will read. These are available in `/etc/apache2/sites-available`. 
By default, there is one site available called _default_ this is what you will 
see when you browse to `http://localhost` or `http://127.0.0.1`. You can have 
many different site configurations available, and activate only those that you need.

As an example, we want the default site to be `/home/user/public_html/`. To do this,
we must create a new site and then enable it in _Apache2_.

To create a new site:

Copy the default website as a starting point. 
`sudo cp /etc/apache2/sites-available/default
/etc/apache2/sites-available/mysite` 

Edit the new configuration file in a text editor `sudo nano` on the command line 
or `gksudo gedit`, for example: 
`gksudo gedit /etc/apache2/sites-available/mysite`

Change the DocumentRoot to point to the new location. 
For example, `/home/user/public_html/`

Change the Directory directive, replace `Directory /var/www/` to `Directory 
/home/user/public_html/`

You can also set separate logs for each site. To do this, change the
_ErrorLog_ and _CustomLog_ directives. This is optional, but handy if you have many sites

Save the file 

Now, we must deactivate the old site, and activate our new one. Ubuntu 
provides two small utilities that take care of this: `a2ensite (apache2enable
site)` and `a2dissite (apache2disable site)`.

`sudo a2dissite default && sudo a2ensite mysite`

Finally, we restart Apache2:

`sudo /etc/init.d/apache2 restart`

If you have not created `/home/user/public_html/`, you will receive an warning
message.

To test the new site, create a file in `/home/user/public_html/`:

`echo '<b>Hello! It is working!</b>' > /home/user/public_html/index.html`

Finally, browse to `http://localhost/`
