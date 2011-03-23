MySQL is a widely used and fast SQL database server. It is a client/server implementation that consists of a server daemon (mysqld) and many different client programs/libraries.

If you want to install Mysql database server in Ubuntu check this tutorial.

What is Mysql Data Directory?

Mysql data directory is important part where all the mysql databases storage location.By default MySQL data default directory located in /var/lib/mysql.If you are running out of space in /var partition you need to move this to some other location.

Note:- This is only for advanced users and before moving default directory make a backup of your mysal databases.

Procedure to follow

Open the terminal

First you need to Stop MySQL using the following command

    sudo /etc/init.d/mysql stop

Now Copy the existing data directory (default located in /var/lib/mysql) using the following command

    sudo cp -R -p /var/lib/mysql /path/to/new/datadir

All you need are the data files, so delete the others with the command

    sudo rm /path/to/new/datadir

Note:- You will get a message about not being able to delete some directories, but that’s what you want.

Now edit the MySQL configuration file with the following command

    gksu gedit /etc/mysql/my.cnf

Look for the entry for “datadir”, and change the path (which should be “/var/lib/mysql”) to the new data directory.

Important Note:-From Ubuntu 7.10 (Gutsy Gibbon) forward, Ubuntu uses some security software called AppArmor that specifies the areas of your filesystem applications are allowed to access. Unless you modify the AppArmor profile for MySQL, you’ll never be able to restart MySQL with the new datadir location.

In the terminal, enter the command

    sudo gedit /etc/apparmor.d/usr.sbin.mysqld

Copy the lines beginning with “/var/lib/mysql”, comment out the originals with hash marks (”#”), and paste the lines below the originals.

Now change “/var/lib/mysql” in the two new lines with “/path/to/new/datadir”. Save and close the file.

Restart the AppArmor profiles with the command

    sudo /etc/init.d/apparmor reload

Restart MySQL with the command

    sudo /etc/init.d/mysql restart

Now MySQL should start with no errors, and your data will be stored in the new data directory location.
