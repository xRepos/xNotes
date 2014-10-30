---
title: Web Crawling Using Node.js
---

Web Crawling Using Node.js
==========================

Crawling
--------

Use ``request`` or ``http`` to get the raw html.

### ``Request``

    #!javascript
    var request = require('request');

    var url = 'http://foo.com';

    # plain text
    request(url, function (err, res, body) {
        ...
    }

    # gzip
    request({url: url, gzip: true}, function (err, res, body) {
        ...
    }


### ``http``

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

Parsing
-------

Use ``cheerio`` to parse html, after that everything works like jQuery.

    #!javascript
    var cheerio = require('cheerio');
    request(url, function(err, res, body){
        $ = cheerio.load(body);
        ...
    }


### Each

    #!javascript
    $('table tr').each(function(i, row) {
        console.log($(this).html())
    });

To get a list of fields, and output the first column

    #!javascript
    $('table tr').each(function(i, row) {
        var fields = $(this).find("td");
        console.log($(fields[0]).text())
    });
