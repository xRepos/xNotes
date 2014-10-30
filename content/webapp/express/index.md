---
title: Express.js
---

Express.js
==========

[Express.js + Angular.js](expressplusangular)

Route
-----

In ``app.js``

    #!javascript
    var routes = require('./routes');

    app.get('/loadData/:name', routes.loadData);

In ``routes/index.js``

    #!javascript
    exports.loadData = function(req, res) {
        console.log(req.route.params.name)
        // or
        console.log(req.params.name)
    }

In browser

    http://127.0.0.1:3000/loaddata/foo

In terminal

    foo


Create a New Project
--------------------

    #!javascript
    $ express --sessions --css less --ejs <myapp>


Enable CORS
-----------

If you see error like:

    XMLHttpRequest cannot load <some_url>. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin '<origin_url>' is therefore not allowed access.

Add the followings to the ``app.js``:

    #!javascript
    app.all('*', function(req, res, next) {
        res.header("Access-Control-Allow-Origin", "*");
        res.header("Access-Control-Allow-Headers", "X-Requested-With");
        next();
    });
