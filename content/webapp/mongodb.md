MongoDB
=======

Configuration File:

    /etc/mongod.conf

Start, stop and restart ``mongod``

    $ sudo service mongod start
    $ sudo service mongod stop
    $ sudo service mongod restart


Check Stats
-----------


    > db.stats()
    {
        "db" : "alertdb",
        "collections" : 10,
        "objects" : 1680137,
        "avgObjSize" : 74.17910801321558,
        "dataSize" : 124631064,
        "storageSize" : 221507584,
        "numExtents" : 44,
        "indexes" : 16,
        "indexSize" : 223229328,
        "fileSize" : 1006632960,
        "nsSizeMB" : 16,
        "dataFileVersion" : {
            "major" : 4,
            "minor" : 5
        },
        "ok" : 1
    }

This method returns the size in bytes for the collection.

    > db.<collection_name>.dataSize()


This method returns the allocation size in bytes, including unused space.
 
   > db.<collection_name>.storageSize()

This method returns the data size, plus the index size in bytes.
 
   > db.<collection_name>.totalSize()

This method returns the index size in bytes.
 
   > db.<collection_name>.totalIndexSize()







Remove Database and Collection
------------------------------

Remove Database:

    > use <database>;
    > db.dropDatabase();

Remove Collection:

    > db.<collection>.remove({})


Count Documents
---------------

    > db.runCommand( { count: '<collection>' } )

Mongoose
--------


    var mongoose = require('mongoose');
    var passport = require('passport');
    var Account = require('./models/account');

    // ...
    // app.use(express.session());
    app.use(passport.initialize());
    app.use(passport.session());
    // app.use(app.router);
    // ...

    passport.use(Account.createStrategy());
    passport.serializeUser(Account.serializeUser());
    passport.deserializeUser(Account.deserializeUser());

    mongoose.connect('mongodb://127.0.0.1/resume');

    app.get('/register', function(req, res) {
        res.render('register', { });
    });

    app.post('/register', function(req, res) {
        Account.register(new Account({ username : req.body.username }), req.body.password, function(err, account) {
            if (err) {
                return res.render('register', { account : account });
            }

            res.redirect('/');
        });
    });

    app.get('/login', function(req, res) {
        res.render('login', { user : req.user });
    });

    app.post('/login', passport.authenticate('local'), function(req, res) {
        res.redirect('/');
    });

    app.get('/logout', function(req, res) {
        req.logout();
        res.redirect('/');
    });