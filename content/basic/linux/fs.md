---
title: File System
---

File System
===========


/var: contains files to which the system writes data during the course of its operation.

* /var/cache (contains cached data from application programs), 
* /var/games (contains variable data relating to games in /usr), 
* /var/lib (contains dynamic data libraries and files), 
* /var/lock (contains lock files created by programs to indicate that they are using a particular file or device), 
* /var/log (contains log files), 
* /var/run (contains PIDs and other system information that is valid until the system is booted again) and 
* /var/spool (contains mail, news and printer queues).

/usr vs /usr/local
------------------

/usr is for software built elsewhere and then installed on the machine (mostly from your distributions package management system) 


/usr/local is for software built locally 




List All Block Devices and Partitions
-------------------------------------

    $ cat /proc/partitions
    major minor  #blocks  name

    253        0   31457280 vda
    253       16   62914560 vdb
    253       32      65536 vdc
    253       48  251658240 vdd

Use ``file -s <device>`` to check type

    $ sudo file -s /dev/vda
    /dev/vda: Linux rev 1.0 ext4 filesystem data, UUID=6f54f78f-3f47-488c-ab1b-b1b8a596c2d3, volume name "c3image-rootfs" (needs journal recovery) (extents) (large files) (huge files)
