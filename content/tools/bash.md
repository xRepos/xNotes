Bash
====

Nohup
-----

Run command in background and redirect output to file.

    nohup command > output & 

Quote from Wikipedia: nohup is a POSIX command to ignore the HUP (hangup) signal, enabling the command to keep running after the user who issues the command has logged out. The HUP (hangup) signal is by convention the way a terminal warns depending processes of logout. Then use

    tail output 

to print the last few lines of the output.

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