jQuery
======

Select on Change
----------------

    #!javascript
    $(selector).change(function() {
        var value = $(this).val();
    })

Disable Form
------------

Disable

    #!javascript
    $('#btn').prop('disabled', true)

Enable

    #!javascript
    $('#btn').removeAttr('disabled');

Input Detect Typing
-------------------

    #!javascript
    $('#foo').keyup()

Window Resize
-------------

    #!javascript
    function windowResize() {
        $('#map_canvas').css('height', function() {return $(window).height() - 50});
    }

    $(window).resize(windowResize);