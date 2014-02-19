---
title: Express.js + Angular.js
description: How to use Express.js on server side and Angular.js on client side
---

Express.js + Angular.js
=======================

This is how I'm doing it... though might not be the best practice

In ``app.js``(server side)

    #!javascript

    // For all the acceptable routes, render ``frame`` anyway, angular will take care of it.
    app.get('/foo/:bar/:baz', function (req, res) {
        res.render('frame');
    })

    // ... and make sure the templates can be rendered independently
    app.get('/templates/:name', function(req, res) {
        res.render('templates/' + req.params.name);
    })

In ``controllers.js``(client side)

    #!javascript
    angular.module('myapp', ['ngRoute', 'ngResource'])
    .config(['$routeProvider', '$locationProvider', function ($routeProvider, $locationProvider) {

        // take care of the routes
        $routeProvider
            .when('/foo/:bar/baz1', {templateUrl: '/templates/baz1', controller: Baz1Ctrl})
            .when('/foo/:bar/baz2', {templateUrl: '/templates/baz2', controller: Baz2Ctrl})

        // this is important ...
        $locationProvider.html5Mode(true);
    }])

and the folder looks like

    project/
    ├───public/
    │   ├───javascripts/
    │   │   └───controllers.js
    │   ├───stylesheets/
    │   └───images/
    ├───views/
    │   ├───templates/
    │   │   ├───baz1.ejs
    │   │   └───baz2.ejs
    │   └───frame.ejs
    └───app.js