Google Maps API
===============

ElevationService
----------------

    #!javascript
    var elevationService = new google.maps.ElevationService();
    elevationService.getElevationAlongPath({path: [], samples: 100}, callback);

Direction Service
-----------------

    #!javascript
    var directionsService = new google.maps.DirectionsService();
    var elevationService = new google.maps.ElevationService();

    var request = {
        origin: getLatLng(route.origin),
        destination: getLatLng(route.destination),
        //waypoints: getWaypoints(route),
        travelMode: google.maps.TravelMode.DRIVING,
        avoidHighways: true
    }

    var rendererOptions = {
        preserveViewport: true,
        map: map,
        polylineOptions: {
            strokeColor: 'steelblue',
            strokeWeight: 5,
            strokeOpacity:1},
        suppressMarkers: true,
        routeIndex: 0
    }

    var directionsDisplay = new google.maps.DirectionsRenderer(rendererOptions);
    directionsService.route(request, function (result, status) {

        if (status == google.maps.DirectionsStatus.OK) {
            directionsDisplay.setDirections(result);
        }
        totalDistance = result.routes[0].legs[0].distance.value / 1000;
        elevationService.getElevationAlongPath({path: result.routes[0].overview_path, samples: 100}, plotElevation);

    });
