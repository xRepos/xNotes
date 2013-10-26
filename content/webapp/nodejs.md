Node.js
=======

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
    http.request({    
        host: 'search.twitter.com', 
        path: '/search.json?' + qs.stringify({ q: search }) 
    }, function (res) {}


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










