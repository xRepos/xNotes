---
title: MySQL
---

MySQL
=====

Install MySQL Server

    $ sudo yum install mysql-server

Start ``mysqld``

    $ sudo /sbin/service mysqld start

Install MySQL

    $ sudo yum install mysql

Login

    $ mysql -u <user_name> -p


Grant
-----

    mysql> CREATEUSER'monty'@'localhost' IDENTIFIED BY'some_pass';
    mysql> GRANTALL PRIVILEGES ON*.*TO'monty'@'localhost'    
        ->     WITHGRANTOPTION;
    mysql> CREATEUSER'monty'@'%' IDENTIFIED BY'some_pass';
    mysql> GRANTALL PRIVILEGES ON*.*TO'monty'@'%'    
        ->     WITHGRANTOPTION;

Error: Another MySQL daemon already running with the same unix socket
---------------------------------------------------------------------

#### Error:

    Another MySQL daemon already running with the same unix socket.
    Starting mysqld:                                           [FAILED]

#### Cause: 

Unexpectedly shutdown the daemon, ``mysql.sock`` is till there.

#### Solution:

Manually remove ``mysql.sock`` file.

    $ sudo mv /var/lib/mysql/mysql.sock /var/lib/mysql/mysql.sock.bak

    $ sudo /sbin/service mysqld start