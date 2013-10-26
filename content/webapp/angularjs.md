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