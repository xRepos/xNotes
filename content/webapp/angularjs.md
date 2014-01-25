---
title: Angular.js
description: Angular.js Notes
---

Angular.js
==========

Loading Data in a Service
-------------------------

    #!javascript
    angular.module('myModule', []) 
        .factory('myService', ['$http', function($http) {
            var item = {};
            $http.get(...).success(function(data) {
                item.foo = data;
            });
            return item;
        }])

    function myController($scope, myService) {
        $scope.item = myService.getItem();
    }

A few notes:

* There is no need to use promise( ``$q`` ) to load data “synchronously”, and there is no need to use $watch to monitor the data, if we are using ``ng-repeat`` or ``ng-model`` angular will automatically watch the changes. The returned value must be an object, not a primitive.
* There is no need to parse the JSON file,  ``$http`` will do it for us, the data received in  success is already a JSON object if the file is json.
* Do not understand why, but it only works if we append the data to a object( ``item.foo = data;`` ) but not if we assign the data directly to the item(this DOES NOT work:  ``item = data`` )

Reuse Bootstrap Modal
---------------------

To reuse the same Modal for displaying different data, put the button and the Modal under the same controller, and use ng-click  to set the data.

E.g. suppose in controller we have

    #!javascript
    function myCtrl($scope) {
        $scope.items = [ {...}, {...}, {...} ];
    }

in html

    #!html
    <div ng-controller="myCtrl">
        <button ng-click="selected=0" data-target="#myModal">Show Item 0</button>
        <button ng-click="selected=1" data-target="#myModal">Show Item 1</button>
        ...
        <div class="modal fade" ...>
            ...
            <div class="model-body">
                {{items[selected]}}
            </div>
        </div>
    </div>

A more complex example:

    #!javascript
    function myCtrl($scope) {
        $scope.items = [ {
            subList: [{name: "foo"}, {name:"bar"],
        }, {
            subList: [],
        }, {
            subList: [],
        }];
    }

then use ``ng-repeat`` to display the subList in the Modal

    #!html
    <div class="model-body">
        <div class="row" ng-repeat="subItem in items[selected].subList">
            {{subItem.name}}
        </div>    
    </div>

Add Listener upon ngView Loaded
-------------------------------

Add this to the controller:

    #!javascript
    $scope.$on('$viewContentLoaded', function() {
        foo();
    })

``$viewContentLoaded`` is the event that "Emitted every time the ngView content is reloaded."

One use case is to resize the components after the view is loaded.


$location
---------
There are two modes of $location in Angularjs. If not set correctly the result might be unexpected.

* HTML5: ``http://foo.com/bar?baz=23#qux``
* Hashbang: ``http://foo.com/#!/bar?baz=23#qux``

The result should be:

* ``$location.path()``: /bar
* ``$location.search()``: baz=23#
* ``$location.hash()``: qux

To use HTML5 model:

    #!javascript
    $locationProvider.html5Mode(true);

For example:

    #!javascript
    angular.module('Foo', ['ngRoute'])
        .config(['$routeProvider','$locationProvider', function($routeProvider, $locationProvider) {
            $routeProvider...
            $locationProvider.html5Mode(true);
        }) 
        ...

$apply and $watch
-----------------

### $apply

Use ``$scope.$apply`` to update bindings:

    #!javascript
    $.ajax({
        url: '/upload',
        type: 'POST',
        success: function(d) {
           
            $scope.$apply(function() {
                $scope.data = d;
            })
   
        },
        ...
    }); 

the ``$scope.data`` in the controller and the references in html (``{{data}}``) should be updated.

### $watch

Use ``$scope.$watch`` to monitor the changes of models.

    #!javascript
    $scope.$watch('foo', function(newVal, oldVal) {
        ...
    });

Or by function(when ``foo`` is in parent's scope for example)

    #!javascript
    $scope.$watch(function() {return $scope.foo;}, function(newVal, oldVal) {
        ...
    });

For example, ``foo`` is loaded from async file read in a parent controller, ``bar`` is a part of ``foo``, ``bar = foo[key]``, and used in the child controller; however ``foo`` is not available at the very beginning, use ``$watch`` to monitor ``foo``, and update ``bar`` when ``foo`` is available:

    #!javascript
    $scope.$watch(function() {return $scope.foo;}, function(newVal, oldVal) {
        if ($scope.key in newVal ) {
            $scope.bar = newVal[$scope.key];
        }
    })

Tabs
----

### Step 1: Model

Use one model(``activeTab``) to control the active tab in controller:

    #!javascript
    function MyCtrl($scope) {
        $scope.activeTab = "tabName1";
    }

### Step 2: Tab
Add controls to the tabs:

* class(``ng-class``) set to ``active`` only if the ``activeTab`` is the current tab
* upon click(``ng-click``), set the ``activeTab`` to the current tab

Code:

    #!html
    <li ng-class="{'active':activeTab=='tabName1'}">
        <a href="#" ng-click="activeTab='tabName1'">tabName1</a>
    </li>

### Step 3: Tab Content

Add controls to the tab content, use ``ng-switch`` and ``ng-switch-when``:

    #!html
    <div class="tab-content">
        <div class="container" ng-switch="activeTab">
            <div ng-switch-when="tabName1">
                asdf
            </div>
            <div ng-switch-when="tabName2">
                qwer
            </div>
        </div>
    </div>


Put everything together:

    #!html
    <div class="container" ng-controller="MyCtrl">
        <ul class="nav nav-tabs nav-justified">
            <li ng-class="{'active':activeTab=='tabName1'}">
                <a href="#" ng-click="activeTab='tabName1'">tabName1</a>
            </li>
            <li ng-class="{'active':activeTab=='tabName2'}">
                <a href="#" ng-click="activeTab='tabName2'">tabName2</a>
            </li>
            ...
        </ul>
        <div class="tab-content">
            <div class="container" ng-switch="activeTab">
                <div ng-switch-when="tabName1">
                    asdf
                </div>
                <div ng-switch-when="tabName2">
                    qwer
                </div>
            </div>
        </div>
    </div>

Beautiful Print Object as JSON
------------------------------

Use ``json`` filter to convert a javascript object to correctly quoted JSON string, and use ``<pre>`` tag to keep the format:

    #!javascript
    <pre>{{myObject | json}}</pre>