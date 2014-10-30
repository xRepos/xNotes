---
title: Nanoc
description: Nanoc solutions
---

Nanoc
=====

Install
-------

### Install Nanoc

    $ gem install nanoc

install dependencies if needed

    $ gem install nokogiri kramdown adsf

then compile by

    $ nanoc
    Loading site data… done
    Compiling site…
          update  [0.07s]  xx/xx/index.html
          ...

    Site compiled in 0.83s.

and serve the website by

    $ nanoc view
    [2014-10-29 14:40:29] INFO  WEBrick 1.3.1
    [2014-10-29 14:40:29] INFO  ruby 2.1.4 (2014-10-27) [x86_64-darwin14.0]
    [2014-10-29 14:40:29] INFO  WEBrick::HTTPServer#start: pid=31613 port=3000

### Install Guard

    $ gem install guard
    $ gem install guard-nanoc

Code Syntax Highlighting
------------------------
Install ``CodeRay``

    $ gem install coderay


Create ``coderay.css``

    $ coderay stylesheet > coderay.css

Add ``filter :colorize_syntax`` to ``Rules``

    #!ruby
    compile '*' do
        filter :kramdown
        filter :colorize_syntax
        layout 'default'
    end

Also the route

    #!ruby
    route '/coderay/' do
        '/coderay.css'
    end

Finally add ``#!language`` to the first line of the code block

Math in Browsers
----------------

Add to layout

    #!javascript
    <script type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">

Change style

    #!css
    .MathJax_Display {
      background-color: ...
      padding: 20px;
      border: 1px solid #DDD;
    }

Check [``MathJax``](http://www.mathjax.org/) for more info
