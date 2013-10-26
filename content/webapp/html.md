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