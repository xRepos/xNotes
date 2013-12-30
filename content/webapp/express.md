---
title: Express.js
description: Express.js Notes
---

Express
=======

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