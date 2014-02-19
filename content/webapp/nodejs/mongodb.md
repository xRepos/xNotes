---
title: Node.js + MongoDB
description: Use MongoDB in Node.js, with either native mongodb or mongoose
---

Node.js + MongoDB
=================

Native MongoDB
--------------

Source Code: [https://github.com/mongodb/node-mongodb-native](https://github.com/mongodb/node-mongodb-native)

Install:

    $ npm install mongodb

### Connect

    #!javascript
    var mongoUrl = 'mongodb://[username:password@]host:[port]/[db]'
    var MongoClient = require('mongodb').MongoClient;

    MongoClient.connect(mongoUrl, function(err, db) {
        if (err) throw err;

        var collection = db.collection('collection_name');

        // do whatever
    })

### Query

    #!javascript
    collection.find({key: value}).toArray(function(err, docs) {
        if (err) throw err;
        
        docs.forEach(function(doc) {
            // do whatever
        })
    })

### Insert

    #!javascript
    collection.insert(entry, function(err, docs) {

    })


Mongoose
--------

Source Code: [https://github.com/LearnBoost/mongoose](https://github.com/LearnBoost/mongoose)

Install:

    $ npm install mongoose