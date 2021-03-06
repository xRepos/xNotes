---
title: Commands
description: A few tips on bash scripts or commands
---


Commands
========


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

udev
----


udev primarily manages device nodes in the /dev directory, Unlike traditional Unix systems, where the device nodes in the /dev directory have been a static set of files, the Linux udev device manager dynamically provides only the nodes for the devices actually present on a system.


    $ ps -e | grep udevd
      304 ?        00:00:00 systemd-udevd



    $ ps -e | grep systemd
      304 ?        00:00:00 systemd-udevd
     1317 ?        00:00:00 systemd-logind





ulimit
------

Per user limit

Check limits

    $ ulimit -a

Check limits by PID

    $ cat /proc/<pid>/limits

Set limits

    $ ulimit -n 64000 -u 64000

* nofile: number of open files
* nproc: number of processes

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



Install Package
---------------

Ubuntu:

    $ dpkg -i filename.deb

Check all installed packages
-----------------------------

    $ dpkg --get-selections
    $ dpkg --get-selections | grep mongo


which vs whereis
----------------

* ``which``: based on PATH

        $ which hadoop
        /Users/myname/lib/hadoop

* ``whereis``: based on standard binary directories

        $ whereis hadoop
        hadoop: /usr/bin/hadoop /etc/hadoop /usr/lib/hadoop /usr/share/man/man1/hadoop.1.gz

Nohup
-----

Run command in background and redirect output to file.

    nohup command > output & 

Quote from Wikipedia: nohup is a POSIX command to ignore the HUP (hangup) signal, enabling the command to keep running after the user who issues the command has logged out. The HUP (hangup) signal is by convention the way a terminal warns depending processes of logout. Then use

    tail output 

to print the last few lines of the output.

Always Search Current Folder First
----------------------------------

Add to ``~/.bashrc`` or ``~/.bash_profile``

    export PATH=`pwd`:$PATH


Style Your Prompt
-----------------

Add to ``~/.bashrc`` or ``~/.bash_profile``

    #!bash
    function prompt {
      local       BLACK="\[\033[0;30m\]"
      local         RED="\[\033[0;31m\]"
      local   LIGHT_RED="\[\033[1;31m\]"
      local       GREEN="\[\033[0;32m\]"
      local LIGHT_GREEN="\[\033[1;32m\]"
      local      YELLOW="\[\033[0;33m\]"
      local        BLUE="\[\033[0;34m\]"
      local     MAGENTA="\[\033[0;35m\]"
      local        CYAN="\[\033[0;36m\]"
      local       WHITE="\[\033[1;37m\]"
      local  LIGHT_GRAY="\[\033[0;37m\]"

      PS1="\n${RED}\u@\h: ${GREEN}\w ${BLACK}\n\$ "
      
    }
    prompt

It should look like:

    <user(red)>@<host(green)>: <working folder>
    $ 

Show Current Git Branch
-----------------------

Add to ``~/.bashrc`` or ``~/.bash_profile``

    #!bash
    function parse_git_branch {
      git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
    }

Then change the last line in ``prompt`` function to

    #!bash
    PS1="\n${RED}\u@\h:${BLUE}\$(parse_git_branch) ${GREEN}\w ${BLACK}\n\$ "


Start and Stop Daemons
----------------------

### Pattern

    #!/bin/bash
    usage="Usage: server.sh (start|stop)"

    # command is 'start' or 'stop'
    command=$1

    case $command in
        (start)
            ...
            ;;

        (stop)
            ...
            ;;

        (*)
            echo $usage
            exit 1
            ;;
    esac

### Get PID

Simple Case: Use pgrep to get pid

    pid_mongod=`pgrep mongod`

Complicated Case: Multiple programs under the same name is running, like Hadoop daemons and Solr daemon are all simply shown as java:

    pid_solr=`ps -eo pid,args | grep 'java -jar start.jar'| grep -v grep | cut -c1-6`

Step by Step:

* ps -e: show all the pids
* ps -o pid,args: specify the fields to show:

    $ ps -eo pid,args
    12498 -bash
    14132 java -jar start.jar
    17489 grep java -jar start.jar
    ...

* grep 'java -jar start.jar': only leave the specified commands:

    $ ps -eo pid,args | grep 'java -jar start.jar'
    14132 java -jar start.jar
    17489 grep java -jar start.jar

* grep -v grep: exclude the grep itself:
    
    $ ps -eo pid,args | grep 'java -jar start.jar'| grep -v grep
    14132 java -jar start.jar

* cut -c1-6: cut the first 6 characters:

    $ ps -eo pid,args | grep 'java -jar start.jar'| grep -v grep | cut -c1-6
    14132

Other ways to get pid: ``echo $$`` or ``echo $!``.

### Start Daemon

    if kill -0 $pid_mongod > /dev/null 2>&1; then
        echo Database is already running ...
    else
        echo Starting Database ...
        bin/mongod &
    fi

Step by Step:

* kill -0 $pid_mongod: -0 for testing if the pid is available to kill. It will return 0 if you can kill <pid>, 1 if <pid> is invalid or you do not have access.
* ... > /dev/null 2>&1: redirect the output to /dev/null, a blackhole. 2 stands for STDERR, 1 for STDOUT. This command means redirect STDOUT to /dev/null, and redirect STDERR to STDOUT(which is /dev/null), so both STDOUT and STDERR will be quiet. Remember the & before destination.
* bin/mongod &: if it is not running, start the daemon. Remember the & for running in the background.
Wait before it is up:

    while true; do
        sleep 1
        if pgrep mongod; then
            break
        fi
    done

### Stop Daemon

Similar to the previous section.
    
    #!sh
    if kill -0 $pid_mongod > /dev/null 2>&1; then
        echo Stopping mongod Server ...
        kill -9 $pid_mongod
    else
        echo No mongod Server to stop ...
    fi

Count Number of Columns
-----------------------

Use `awk`:

    $ cat file | head -1 | awk -F"," '{print NF}'

Create Symbolic Link
--------------------

    $ ln -s 0.1.0-SNAPSHOT/ snapshot
    $ ls -l
    ... snapshot -> 0.1.0-SNAPSHOT/

Cron
----

``/etc/crontab`` schedules ``/etc/cron.hourly``, ``/etc/cron.daily``, ``/etc/cron.weekly``, ``/etc/cron.monthly``.

Scripts in those folders will be executed.

By default cron jobs logs can be found in ``/var/log/syslog``

    $ grep CRON /var/log/syslog

Add Timestamp to Filename
-------------------------

To show timestamp in a specific format, use the format string like ``+"%Y%m%d"``

    $ date +"%Y%m%d"
    20140220

For more format strings, check ``$ date --help``. To use timestamp in a filename:

    $ echo "hello" > `date +"%Y%m%d"`.log
    $ cat 20140220.log
    hello

Redirect StdErr to StdOut
-------------------------

    $ do whatever > /home/ubuntu/`date +"%Y%m%d"`.log 2>&1

2>&1 indicates that the standard error (2>) is redirected to the same file descriptor that is pointed by standard output (&1).

Check If Command Exists
-----------------------

    $ command -v foo >/dev/null 2>&1
    $ type foo >/dev/null 2>&1
    $ hash foo 2>/dev/null

Example: add HADOOP_CLASSPATH if ``hadoop`` exists

    command -v hadoop > /dev/null && {
        HADOOP_CLASSPATH=`hadoop classpath`
        CLASSPATH=$HADOOP_CLASSPATH:$CLASSPATH
    }

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

