---
title: Node.js
description: Node.js Notes
---

Node.js Index
=============

[Node.js + MongoDB](mongodb)

Stringify
---------

To pretty print(indent by 4 spaces):

    #!javascript
    JSON.stringify(data, null, "    ")

Web Crawling and Parsing
------------------------

Here is a quick way for crawling and parsing. Use ``request`` to get the raw html and ``cheerio`` to parse, after that everything works like jQuery.

    #!javascript
    var request = require('request');
    var cheerio = require('cheerio');
    var url = 'http://foo.com';
     
    request(url, function(err, res, body){
      $ = cheerio.load(body);
      console.log(body);
    });

Or use ``http``

    #!javascript
    var http = require('http');
    http.request({    
        host: 'search.twitter.com', 
        path: '/search.json?' + qs.stringify({ q: search }) 
    }, function (res) {}

If plain text

    #!javascript
    http.get(url, function(res){
        var buffer = [];
        res.on('data', function(data) {
            buffer.push(data);
        }).on("end", function() {
            parsePage(buffer.join(''));
        })
    });

If gziped

    #!javascript

    var zlib = require('zlib');

    http.get(url, function(res){
      
        var buffer = [];
        var gunzip = zlib.createGunzip();            
        res.pipe(gunzip);

        gunzip.on('data', function(data) {
            buffer.push(data);
        }).on("end", function() {
            parsePage(buffer.join(''));
        })
    });

Commandline Arguments
---------------------

Commandline arguments are stored in ``process.argv``. Try

    # test.js
    console.log(process.argv)

from commandline

    $ node test.js foo
    [ 'node',
      '/path/to/test.js',
      'foo' ]


File Upload
-----------

HTML

    #!html
    <input id="file-upload" type="file" name="foo" />

Where “id” is used for jQuery selector to find this div, and “name” is used for looking for the file(there could be multiple files, identified by names).

Server
    
    #!javascript
    exports.uploadFile = function(req, res) {
        var html = fs.readFileSync(req.files.foo.path);
        // ...
        res.json({...});
    }

``req.files`` is a collection of files, if the filename is “foo”, then the info about this file is stored in ``req.files.foo``, and ``req.files.foo.path`` is a local temporary path storing the uploaded file. Add the POST to app:

    app.post('/uploadFile', yourModule.uploadFile);

jQuery

    #!javascript
    $('#btn-upload').click(function(){
        var data = new FormData();
        data.append('foo', $('#file-upload')[0].files[0]);

        $.ajax({
            url: '/uploadFile',  
            type: 'POST',
            success: function(d) {console.log(d)},
            error: function() {console.log("error")},
            data: data,
            cache: false,
            contentType: false,
            processData: false
        });
    });

To get the file from the ``<input>``, use ``$('#file-upload')[0].files[0]``

The success callback will receive whatever the server returned.

Read/Write File
---------------

Read file, ``fs.readFile`` will read file as binary

    #!javascript
    var data = fs.readFileSync('data.json');
    console.log(data);
    //<Buffer 7b 22 32 30 30 30 22 3a 5b 7b 22 52 61 6e 6b 22 3a 31 2c 22 41 69 72 70 6f 72 74 22 3a 22 20 48 61 72 74 73 66 69 65 6c 64 2d 4a 61 63 6b 73 6f 6e 20 41 ...>

Use ``.toString()`` to get String

    #!javascript
    var str = fs.readFileSync('data.txt').toString();

Use ``JSON.parse()`` to get JSON

    #!javascript
    var data = JSON.parse(fs.readFileSync('data.json'));

Write file, use ``JSON.stringify()``

    #!javascript
    fs.writeFile("filename.json", JSON.stringify(data));

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


Req Lookup
----------

### Params

Params are stored as

    #!javascript
    req.route.params.<param_name>

E.g. in ``app.js``:

    #!javascript
    app.get('/foo/:name', ...)

A request to ``/foo/bar`` will generate

    #!javascript
    req.route.params.name == 'bar'

### File Upload

Uploaded files

    #!javascript
    req.files.<file_name>.path

### Data Upload

Uploaded data

    #!javascript
    req.body.<data_name>

``req.files`` and ``req.body`` are available for POST requests, but not GET requests

E.g. use ``Angular.js``:

    #!javascript
    $http.get('/someUrl').success(successCallback);
    $http.post('/someUrl', data).success(successCallback);

Global Object
-------------

* Browser: ``window``
* Server: ``process``
    * ``process.env``: env defined and exported in ``~/.bash_profile`` or ``~/.bashrc``



Module
------

### Load a module:

Search from ``node_modules``:

    #!javascript
    require("module_name");

Search from file:

    #!javascript
    require("./module_name");
    require("/path/to/model_name");

### Write a module, use ``exports``

    #!javascript
    // in module
    exports.foo = 10

    // outside module
    var bar = require("./module_name");
    console.log(bar.foo); // 10


npm install
-----------

Save to ``package.json`` - ``dependencies`` section: 

    $ npm install --save <package-name>

Save to ``package.json`` - ``devDependencies`` section: 

    $ npm install --save-dev <package-name>


Quick Lookup
------------

Get num of CPUs:

    #!javascript
    var numCPUs = require('os').cpus().length;

