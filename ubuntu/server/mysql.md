### Recover mysql root password 

1. sudo service mysql stop

2. sudo mysqld\_safe --skip-grant-tables &

3. mysql -u root mysql

4. mysql> update user set password=PASSWORD('your\_password') where User='root';

5. mysql> flush privileges;

6. mysql> quit;

7. kill -9 pid(mysqld\_safe)

8. sudo service mysql start

9. mysql -u root -p 

### Change mysql root password

* mysqladmin -u root -p'old\_password' password new\_password

To setup root password for the first time, then use following command:

* mysqladmin -u root password new\_password
