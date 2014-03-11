### Recover mysql root password 

    sudo service mysql stop

    sudo mysqld_safe --skip-grant-tables &

    mysql -u root mysql

    mysql> update user set password=PASSWORD('your_password') where User='root';

    mysql> flush privileges;

    mysql> quit;

    kill -9 pid(mysqld_safe)

    sudo service mysql start

    mysql -u root -p

### Change mysql root password

    mysqladmin -u root -p'old_password' password new_password

To setup root password for the first time, then use following command:

    mysqladmin -u root password new_password

### export data from db

    mysqldump -uroot ec_production > ec_production.sql

### import data to database

    mysql -uroot ec_development<ec_development.sql

### resources

* <http://www.sitepoint.com/optimizing-mysql-application/>
