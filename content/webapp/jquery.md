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

To resize any part of the page upon window resize:

    #!javascript
    function windowResize() {
        $('#map').height($(window).height() - 50);
    }
    $(window).resize(windowResize);

Or

    #!javascript
    function windowResize() {
        $('#map').css('height', function() {return $(window).height() - 50});
    }

    $(window).resize(windowResize);



