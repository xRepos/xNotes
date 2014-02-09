---
title: Javascript
description: Tips on programming javascript
---

Javascript
==========


Set default value inside function
---------------------------------

    #!javascript
    function foo(params) {
        var settings = params || {}
    }

Get Object keys
---------------

    #!javascript
    Object.keys(obj)

Get Max/Min of an Array
-----------------------

``Math.max`` and ``Math.min`` do not work on arrays, for example ``Math.max(1,2,3,4)``. To get the max/min of an array, use ``apply`` 

    #!javascript
    Math.max.apply(Math, [1,2,3,4])
    Math.min.apply(Math, [1,2,3,4])

in vs. hasOwnProperty()
-----------------------

* ``in``: check prototype chain, all inherited properties will be included.
* ``hasOwnProperty()``: only check its own properties.


Merge Options with Default
--------------------------

    #!javascript
    var getMergedOptions = function(options, defaults) {
        var options = options || {}, 
            option;

        for(option in defaults) {
            if(defaults.hasOwnProperty(option) && !options[option]) {
                options[option] = defaults[option];
            }
        }

        return options;
    }

Regular Expression
------------------

### Literal vs. Constructor

* Literal: ``re = /.../g``
* Constructor: ``re = new RegExp("...")``
    * can use string concat: ``re = new RegExp("..." + some_variable + "...")``

### Local vs. Global

* ``re = /.../``: ``re.match(str)`` will return a list of captures of the FIRST match
* ``re = /.../g``: ``re.match(str)`` will return a list of matches but NOT captures

### match vs. exec

* ``match``: as stated above
* ``exec``: return captures, exec multiple times

Example

    #!javascript
    var match;
    while ((match = re.exec(str)) !== null) {

    }

### Use jQuery

* Match Text: 
    * ``re.exec($(selector).text())``
    * ``$(selector).text().match(re)``
* Match HTML:
    * ``re.exec($(selector).html())``
    * ``$(selector).html().match(re)``

Date
----

    #!javascript
    var date = new Date();

    // date
    date.getDate();

    // month(0-11)
    date.getMonth() + 1;

    // year(201x)
    date.getFullYear();

    // get previous day 
    date.setDate(date.getDate() - 1)
