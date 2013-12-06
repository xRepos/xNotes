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