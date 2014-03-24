Load Linkedin Data To Scope
===========================


Specify ``api_key`` and ``onLoad`` function

    #!html
    <script type="text/javascript" src="http://platform.linkedin.com/in.js">
        api_key: <here goes the api key>
        onLoad: onLinkedInLoad
        authorize:true
    </script>

``onLoad`` function

    #!javascript
    //execute on login event
    functionon onLinkedInLoad() {
        
        angular.element(document.getElementById("body")).scope().$apply(
            function($scope) {
                $scope.getLinkedInData();
            });
    }

Inside ``$scope``

    #!javascript
    $scope.getLinkedInData = function () {
        IN.Event.on(IN, "auth", onLinkedInAuth);
    }

    function onLinkedInAuth() {
        IN.API.Profile("me")
            .fields("id","firstName", "lastName","headline","industry","summary","positions","picture-url","educations","skills","certifications","patents","honors-awards","languages","publications","projects","phone-numbers","email-address","main-address","public-profile-url")
            .result(function(result) {
                $scope.$apply(function() {
                    $scope.profile = result.values[0]
                    console.log($scope.profile)
                })

            });
    }