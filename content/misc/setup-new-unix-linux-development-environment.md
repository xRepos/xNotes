---
title: Setup New Environment
---


Setup New Linux/Unix Environment
================================

* ~/.vimrc
* ~/.bash_profile
* ~/.ssh/config
* install packages

~/.vimrc
--------

    syntax on
    set ts=4
    set shiftwidth=4
    set expandtab

Add syntax highligh

    syntax on

Use soft tab(spaces instead of tabs)

    set expandtab

~/.bash_profile
---------------

### ``ls``: color by file extension

To show colors by file extension

    $ ls -G

To make it default, add this to ``~/.bash_profile``

    alias ls="ls -G"

### Style your bash

Note: in Mac OS X, open Terminal->Preferences, choose "Shells open with" as "Command(complete path)", and set it ``bin/bash`` to use ``~/.bash_profile`` settings.

    function prompt {
        local      BLACK="\[\033[0;30m\]"
        local        RED="\[\033[0;31m\]"
        local  LIGHT_RED="\[\033[1;31m\]"
        local      GREEN="\[\033[0;32m\]"
        local LIGHT_GREEN="\[\033[1;32m\]"
        local      YELLOW="\[\033[0;33m\]"
        local        BLUE="\[\033[0;34m\]"
        local    MAGENTA="\[\033[0;35m\]"
        local        CYAN="\[\033[0;36m\]"
        local      WHITE="\[\033[1;37m\]"
        local  LIGHT_GRAY="\[\033[0;37m\]"

        PS1="\n${RED}\u@\h:${BLUE}\$(parse_git_branch) ${GREEN}\w ${BLACK}\n\$ "
    }
    prompt

~/.ssh/config
-------------

    Host <alias>
        HostName <host_name or IP>
        User <user_name>
        IdentityFile /path/to/private/key.pem

For example

    Host foo
        HostName 10.xxx.xxx.xxx
        User stack
        IdentityFile /path/to/private/key.pem

then

    $ ssh foo

is essentially the same as

    $ ssh -i /path/to/private/key.pem stack@10.xxx.xxx.xxx

Install Packages
----------------

### Mac OS X

#### Install HomeBrew

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

HomeBrew will install packages to ``/usr/local/Cellar``, the default library is ``/Library``.

For example, if install ruby by ``homebrew``

    $ brew install ruby

Ruby will be installed in ``/usr/local/Cellar/ruby``, though the default ruby is installed in ``/Library/Ruby/Site``

#### Install Node.js

    $ brew install nodejs

#### Ruby and Gem

Install ruby

    $ brew install ruby

Upgrade gem


    $ gem update --system
    Updating rubygems-update
    ...

Update installed gems

    $ gem update
    Updating installed gems
    ...
