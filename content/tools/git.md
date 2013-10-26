Git
===

Config
------

Config file location:

* Global: ``~/.gitconfig``
* System: ``/etc/gitconfig``
* Local: ``/git/config``coding

Set a name

    $ git config --global user.name "My Name"
    $ git config --local user.name "Foo Bar"
 
Show the name

    $ git config --local user.name
    Foo Bar