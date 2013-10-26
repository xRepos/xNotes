Git
===

Config
------

Global config: in your home directory
    
    $ vim ~/.gitconfig

Local config: inside repository directory

    $ vim .git/config

Set a name

    $ git config --global user.name "My Name"
    $ git config --local user.name "Foo Bar"
 
Show the name
   
    $ git config --local user.name
    Foo Bar