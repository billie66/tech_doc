### The MySQL database package consists of the following:

* The MySQL server: This is the heart of MySQL. You can consider it a program 
that stores and manages your databases.

* MySQL client programs: MySQL comes with many client programs. The one with which 
we'll be dealing a lot is called mysql (note: smallcaps). This provides an 
interface through which you can issue SQL statements and have the results displayed.

* MySQL client Library: This can help you in writing client programs in C. 
(We won't be taking about this in our tutorial).

### The difference between MySQL and mysql

MySQL is used to refer to the entire MySQL distribution package or the MySQL server
, while mysql refers to a client program.

### Why have client and server programs?

The server and client programs are different entities.
Thus, you can use client programs on your system to access data on a MySQL server 
running on another computer. 

(Note: you would need appropriate permissions for this. 
Consult the system administrator of the remote machine.)

Dividing the package into a server and clients separates the actual data from the interface.
