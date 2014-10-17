Linux
=====

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


Install Package
---------------

Ubuntu:

    $ dpkg -i filename.deb


Manual
------

* Section 1: user commands 
* Section 2: system calls 
* Section 3: library functions
* Section 4: special files
* Section 5: file formats
* Section 6: games
* Section 7: conventions and miscellany
* Section 8: administration and privileged commands
* Section L: math library functions
* Section N: tcl functions

e.g.

    $ man 8 mount


Hostname
--------

* ``/etc/hostname``: the hostname of the machine
* ``/etc/hosts``: list of hosts
* ``host <host_name>``: DNS lookup

Unknown Host Error in ``sudo``: make sure the names match

    $ cat /etc/hosts
    127.0.1.1   example-hostname

    $ cat /etc/hostname
    example-hostname

    $ host example-hostname
    example-hostname.foo.bar.example.com has address 10.64.209.136

Check all installed packages
-----------------------------

    $ dpkg --get-selections
    $ dpkg --get-selections | grep mongo


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

Format a Device
---------------

Use ``mkfs.ext2``, ``mkfs.ext3``, ``mkfs.ext4`` etc

    $ sudo mkfs.ext3 /dev/<device>

Check FS
--------

    # df -hT | awk '{print $1,$2,$NF}' | grep "^/dev"
    /dev/sda3 ext4 /
    /dev/sda2 ext2 /boot
    /dev/sda6 ext4 /tmp
    /dev/sdb1 ext4 /data1
    /dev/sdc1 ext4 /data2
    /dev/sdd1 ext4 /data3

Mount / Umount
--------------

Assume a device is added as ``/mnt/vdc``. Create new folder as ``/dev/vdc``

    $ sudo mkdir /dev/vdc 

Edit ``/etc/fstab``.

    # <file system> <mount point>   <type>  <options>       <dump>  <pass>
    /dev/vdc        /mnt/vdc        auto    defaults        0       0

Mount all

    $ sudo mount -a

Check by ``df``

    $ df
    Filesystem     1K-blocks    Used Available Use% Mounted on
    /dev/vdc           65390      36     65354   1% /mnt/vdc


To remount

    $ mount -o remount /dev/vdc

umount: it seems [device] is mounted multiple times
---------------------------------------------------

Error: 

    $ umount /dev/[device] 
    umount: it seems /dev/<device> is mounted multiple times

Solution: use sudo

    $ sudo umount /dev/[device]
