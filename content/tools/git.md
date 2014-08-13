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

Checkout a Remote Branch
------------------------

    $ git fetch
    $ git checkout test

or 


    $ git checkout -b <branch> --track <remote>/<branch>



Tags
----

List all tags:

    $ git tag -l

Checkout a tag:

    $ git checkout tags/<tag_name>

Remove a remote tag:

    $ git push origin :refs/tags/<tag_name>

Remove a local tag:

    $ git tag -d <tag_name>

Add All
-------

To add everything to stage, including additions and removals, use 

    $ git add -A


Abandon Changes
---------------

Abandon changes and revert your tree to the "clean" state of your current branch. Don't use 'git revert', use:

    $ git reset --hard HEAD 

Reset to a remote branch

    $ git fetch origin
    $ git reset --hard origin/master

Mac OS X Uses Wrong Git Account
-------------------------------

If multiple GitHub accounts are logged in using Mac OS X, the account info might be stroed by Keychain Access. Maven release plugin may fails for using wrong Github account.

    [ERROR] Provider message:
    [ERROR] The git-push command failed.
    [ERROR] Command output:
    [ERROR] remote: Permission to <...>/<...>.git denied to <...>.
    [ERROR] fatal: unable to access 'https://github.com/<...>/<...>.git/': The requested URL returned error: 403

Solution: find Keychain Access in spotlight or by

    Applications->Utilities->Keychain Access.app

Search for ``github`` and remove the records. 

Upstream Remote
---------------------

Add your own fork as ``origin`` remote

    $ git remote add origin https://github.com/<your_fork>/<project_name>.git
    
Add the central repo as ``upstream`` remote

    $ git remote add upstream https://github.com/<central_repo>/<project_name>.git

To sync up with ``upstream``

    $ git fetch upstream
    $ git merge upstream/develop 

Or 
    
    $ git pull upstream develop


