start mysql (three methods):

* /etc/init.d/mysql restart

* mysql -u root

* mysql -u root -p 

set password:

    mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('yourpassword');

quit mysql:

    mysql> \q;  

create a database:

    mysql> create database databasename;

delete the existed database.

    mysql> drop datebase databasename;||drop schema databasename;

create tables:

    mysql> show databases;
    mysql> use dbname;
    mysql> show tables;
    mysql> create table tablename();

describe table:

    mysql> describe tablename;

For example:

    mysql> CREATE TABLE grocery_inventory (
        -> id int not null primary key auto_increment,
        -> item_name varchar (50) not null,
        -> item_desc text,
        -> item_price float not null,
        -> curr_qty int not null
        -> );

For example:

    mysql>use mysql;
    mysql>select * from  person;
    mysql> insert into person (id,firstname,lastname) values(106,'peter','wang');


Note:don't forget a semicolon(;) at the end of the statements.

    mysql> GRANT ALL PRIVILEGES ON *.* TO 'yourusername'@'localhost' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;

This instruction is to add a new user who has all privileges

    mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON database1.* TO 'yourusername'@'localhost' IDENTIFIED BY 'yourpassword';

Above statement for crating a new user with fewer privileges(should work for 
most web applications) which can only use database named _database1_

There is a good web address to learn [SQL][SQL tutorial].

[SQL tutorial]: http://www.webdevelopersnotes.com/tutorials/sql/index.php3 

