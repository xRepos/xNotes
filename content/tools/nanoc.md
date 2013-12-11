---
title: Nanoc
description: Nanoc solutions
---

Nanoc
=====

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

