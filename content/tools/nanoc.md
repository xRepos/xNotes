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