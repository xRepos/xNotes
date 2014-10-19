Variables
=========

* ``$#`` - Denotes the number of arguments you have passed to the shell script from the command line.

* ``$@`` - All arguments, as separate words.

* ``$*`` - All arguments, as one word.

* ``$$`` - ID of the current process.

* ``$?`` - Exit status of the last command.

* ``$0,$1,..$9,${10},${11}…${N}`` - These are positional parameters. After “9″ you must use the ${k} syntax.

* ``HOME`` - Home directory of the user.

* ``MAIL`` - Contains the path to the location where mail addressed to the user is stored. 

* ``IFS`` - Contains a string of characters which are used as word seperators in the command line. The string normally consists of the space, tab and the newline characters. To see them you will have to do an octal dump as follows:

        $ echo $IFS | od -bc

* ``PS1 and PS2`` - Primary and secondary prompts in bash. PS1 is set to $ by default and PS2 is set to > . To see the secondary prompt, just run the command :

        $ ls |

... and press enter.

* ``USER`` - User login name.

* ``TERM`` - indicates the terminal type being used. This should be set correctly for editors like Vim to work correctly.

* ``SHELL`` - Determines the type of shell that the user sees on logging in.




Show Login Name
---------------

    $ echo $LOGNAME
    stack





Enviroment Variables
--------------------

List all variables

    $ env
    TERM=xterm-256color
    SHELL=/bin/sh
    JAVA_HOME=...
    HADOOP_HOME=...

    $ printenv

Remove variable

    $ unset <VAR_NAME>