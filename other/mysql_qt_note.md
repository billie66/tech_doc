Today is June 10,2009.

It is a wonderful day.I successfully makes QT communicating with MySQL server.
What a exhilarating thing it is!I feel very delighted. I am so lucky that I 
didn't encounter those errors which other newbies met with. I succeed fortunately.

I think that I must record the procedures. If not, maybe I will forget how to. 
At the beginning, I have no idea about it. I just know the QT built in my OS 
without MySQL or SQLITE support. So I must reconfigure,recompile and reinstall 
QT with MySQL support.

The processes as follows:

Firstly, install MySQL sever/client database in ubuntu as'root' account

	apt-get install mysql-server 
	apt-get install mysql-client //also alternative with one line command

The default directory is `/var/local/mysql`
view .cnf file in /etc/mysql/my.cnf. Executing above directives can install MySQL database.

Secondly, In order to connect QT to MySQL, must install `libmysqlclient15-dev`package,
which comprises the necessary header files.

    apt-cache search mysql  /* search useful packages about mysql */

Then find the needed package `libmysqlclient15-dev`. The version(here is 15) 
is different in various OS.

    apt-cache show packageName  /* display informations about packageName */

In my OS, the packageName is `libmysqlclient15-dev`. This is exactly what I need.

    apt-get install libmysqlclient15-dev

execute it, the directories `/usr/include/mysql` and `/usr/lib/mysql` appear.
It is a good sign.
Must use these two folders to reconfigure QT.

Thirdly, now all works have been prepared, I am able to reconfigure QT. 

    make confclean
    ./configure -prefix /d/QT -plugin-sql-mysql -I/usr/include/mysql -L/usr/lib/mysql -v
    make 
    make install

After execute above commands, the QT installed with MySQL and SQLITE MySQL3 support

Fourthly, I am not sure whether I have built QT with MySQL support. So I check
it though `sqlbrowser` example.

Luckily, running `sqlbrower` the result display QMYSQL driver. I still suspect it.

Furtherly, I recompile `/d/QT/example/sql/tablemodel` example. Badly, many errors occur!
When I see so many errors, I am afraid that QT was reconfigured wrongly. If so, 
I don't know how to do, since I have searched many google webpages about this issue. 
Only Qt-interest meet my flavour.

For projects that use the SQL classes, I remember that a line `QT +=sql` must 
be added to its `.pro` file. This will ensure the application is linked against
the QtSql library. Incrediably, all errors disappear after recompiled and the 
programme can run connecting to QSQLITE database.

I modify the tablemodel example and rewrite connect.h file.

I change `QSqlDatebase db=QSqlDatebase::addDatebase("QSQLITE");` to
`QSqlDatebase db=QSqlDatebase::addDatebase("QMYAQL")`;

Then recompile and run,but pop up a error dialog.

Fifthly, I modify connection.h file again. Add the following statements and 
remove some nonuseful statements.

     db.setHostName("localhost");
     db.setDatabaseName("mysql");
     db.setUserName("root");
     db.setPassword("");

Recompile the example and run correctly, I succeed finally. Since MySQl created 
a default database named `mysql`, when I installed MySQL as root account on local 
and I didn't set up passward with mysql database.

This example verifies MySQL driver has been loaded successfully. QT can support MySQL database.

Note:  Above four statements must be setted up correctly otherwise QT cann't connect to MySQL.
I have tried varied settings in which only above setting is valid.
This means a datebase must has been created if QT want to communicate with it.  

PS:  configuration

    ubuntu8.04 LST
    qt-x11-opensource-src-4.4.3
    MySQL

