---
title: SSH
---

SSH
===

The So-called Password-less SSH
-------------------------------

I was confused by this for a long time...

The key concept here is the ``Keypair``, it is called a "pair" so there must be two files: one public and one private. Local machine has the private one, and remote machine has the public one, if somehow they match, you are connected!

* Remote: the public keys are stored in ``~/.ssh/authroized_keys``. Yes the "keys", it can have not only your public key but also tons of others.
* Local: use ``ssh -i myPrivateKey foo@baz`` to specify which private key to use(in this case ``myPrivateKey``)
    * if you are using Amazon AWS, OpenStack or others of the kind, you probably will get a file like ``Keypair.pem`` from the platform, it is actually a private key.
    * if you are using ``ssh-keygen``, 2 files will be generated, the one without ``.pub`` is the private key

And here is the magic: if you do not specify which private key file to use("-i"), ssh will look for the file ``~/.ssh/id_rsa``!

Specify IdentityFile for Host
-----------------------------

To specify an IdentityFile other than the default, edit ``~/.ssh/config``

    Host heroku.com
        HostName heroku.com
        IdentityFile /path/to/another/private-key

when you use git to talk to the remote repository ``git@heroku.com:myapp.git``, it will use the specified key instead.