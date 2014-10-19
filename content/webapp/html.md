---
title: xNotes - HTML CSS
---

HTML/CSS
========

Code Syntax Highlighting
------------------------

Add this to ``<head>``

    #!html
    <link href='http://google-code-prettify.googlecode.com/svn/trunk/src/prettify.css' rel='stylesheet' type='text/css'/>
    <script src="http://google-code-prettify.googlecode.com/svn/trunk/src/prettify.js" type="text/javascript">

Edit ``<body>``

    #!html
    <body onload='prettyPrint()'>

Add code block

    #!html
    <pre class="prettyprint lang-html">
    ...
    </pre>

Language Options: (use lang-):
"bsh", "c", "cc", "cpp", "cs", "csh", "cyc", "cv", "htm", "html", "java", "js", "m", "mxml", "perl", "pl", "pm", "py", "rb", "sh", "xhtml", "xml", "xsl"

Open Link in New Tab
--------------------

    #!html
    <a href="..." target="_blank">...</a>

CSS Grayscale
-------------


    #!css
    img {
      -webkit-filter: grayscale(0.5) blur(10px);
    }

Set grayscale to 1 to show grayscale image(no color), 0 to hide grayscale effect