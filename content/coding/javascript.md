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

in vs. hasOwnProperty()
-----------------------

* ``in``: check prototype chain, all inherited properties will be included.
* ``hasOwnProperty()``: only check its own properties.

    function applyDefaults(params, defaults) {
    var settings = params || {};

    for(var setting in defaults) {
      if(defaults.hasOwnProperty(setting) && !settings[setting]) {
        settings[setting] = defaults[setting];
      }
    }

    return settings;
  }