How to Build the QMYSQL Plugin on Unix (ubuntu9.04 + qtcreator + mysql5)

This article is about how to make qtcreator support mysql

You need the MySQL header files and as well as the shared library
`libmysqlclient.so`. Depending on your Linux distribution you may need to 
install a package which is usually called `mysql-devel`.

Tell qmake where to find the MySQL header files and shared libraries. Here 
it is assumed that _MySQL_ is installed in `/usr/local` and run _make_:

    cd $QTDIR/src/plugins/sqldrivers/mysql
    qmake "INCLUDEPATH+=/usr/include/mysql" "LIBS+=-L/usr/lib -lmysqlclient_r" mysql.pro
    make

Then generate libqsqlmysql.so shared library

After installing Qt, as described in the `Installing Qt on X11 Platforms` document, 
you also need to install the plugin in the standard location:

    cd $QTDIR/src/plugins/sqldrivers/mysql
    make install

This step will install `libqsqlmysql.so` in
`/opt/qtsdk-2009.03/qt/plugins/sqldrivers/`.

Then move `libqsqlmysql.so` to `/opt/qtsdk-2009.03/bin/sqldrivers/`.

After above mentioned procedures, you have to add some statements in
_connection.h_ file
    
    QSqlDatabase db = QSqlDatabase::addDatabase("QMYSQL");
    db.setHostName("localhost");
    db.setDatabaseName("mysql");
    db.setUserName("root");
    db.setPassword("111111");

Finally _qtcreator_ can communicate with _mysql_.
