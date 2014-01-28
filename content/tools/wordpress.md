---
title: xNotes - WordPress
description: WordPress
---


WordPress
=========

Even though I migrated from WordPress to Nanoc, I'm putting this note here in case I need to setup another WordPress site.

Setup MySQL
-----------

Show all the databases

    mysql> show databases;

Create a new database

    mysql> CREATE DATABASE <dbname>;

Show all the users

    mysql> select host, user, password from mysql.user;

Create a new user

    mysql> CREATE USER '<username>'@'localhost' IDENTIFIED BY '<password>';

Grant privileges

    mysql> GRANT ALL PRIVILEGES ON *.* TO '<username>'@'localhost';

Open blog in browser for the first time, fill in the form to connect to db; make a copy of the generated config file to ``wp-config.php``

Install plugins
---------------

Download Plugin, make a copy in ``wp-content/plugins``
Open "Plugins" tab in admin page, activate