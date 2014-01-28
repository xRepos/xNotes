---
title: xNotes - Java
description: Java Notes
---

Java
====

Details
-------

### parseDouble vs valueOf

* ``Double.parseDouble(String s)`` returns ``double`` (the primitive)
* ``Double.valueOf(String s)`` returns ``Double`` (the object)

Some tests

    #!java
    System.out.println(Double.valueOf("Infinity"));
    //Infinity

    System.out.println(Double.valueOf("-Infinity").isInfinite());
    //true

    System.out.println(Double.valueOf("NaN"));
    //NaN

    System.out.println(Double.MAX_VALUE);
    //1.7976931348623157E308


    System.out.println(Double.MAX_VALUE + Double.MAX_VALUE);
    //Infinity

### Date Conversions

Step 0: Import

    #!java
    import java.text.SimpleDateFormat;
    import java.util.Date; 

Step 1. Define format

    #!java
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss"); 

Step 2. Conversions

    #!java
    //String -> Date
    Date d = sdf.parse("2011/12/04 00:00:00");

    //Date -> String
    String dateTimeString1 = sdf.format(new Date());
    String dateTimeString2 = sdf.format(System.currentTimeMillis()));
    //Long -> Date
    Date d = new Date(System.currentTimeMillis());

    //Date -> Long
    long time = d.getTime();

### Hex

Imaging a concatenated string using 0x7f as delimiter, we could split it in two easy ways:

    #!java
    char delimiter = 0x7f;
    String [] vals = line.split(Character.toString(delimiter));


or simply:

    #!java
    String [] vals = line.split("\\x7f");


However it is a different story to join them. It is ok like this:

    #!java
    String s = "";
    for (String v : vals) {
        s += v + delimiter; 
    }


but if use

    #!java
    s += v + "\\x7f";


it will add 4 character after each v: \, x, 7, f, instead of a hex 0x7f, and hence could not split it again as we discussed above.


Error Log
---------

### java.net.UnknownHostException

Got the error message when using Mac OS X + Java 7

java.net.UnknownHostException: ComputerName: ComputerName: nodename nor servname provided, or not known
Solution: add

    127.0.0.1  ComputerName

to

    /etc/hosts

Maven
-----

### Install Third-Party Packages on Maven

    $ mvn install:install-file -Dfile=<path-to-file>
        -DgroupId=<group-id> -DartifactId=<artifact-id> 
        hadoophadoop-Dversion=<version> -Dpackaging=<packaging>

