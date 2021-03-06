google-map-animation
====================
The idea is simple: We need to do animation between two place on google map, respecting the estimated time and the route provided from the google direction api. The module takes care of following things.

<ul>
    <li>On road plotting of marker</li>
    <li>Smooth Animation</li>
    <li>Animation would always respect estimated time returned by google direction api.</li>
</ul>

This module can be simply included in your app and by configuring and injecting it you can make it working for you.

**Requirements:** AngularJS v1.4.11+

## Usage:

1.include all the dependencies which are needed to make animation work, following component and libraries are needed as pre-requisite.
    
#### via bower:
```
$ bower install angular-google-maps
$ bower install jquery-easing
$ bower install epoly-v3 
```
    
#### via npm:
```
$ npm install angular-google-maps
$ npm install jquery-easing
```
    
#### once the library is installed, include it:
```html
<script src="bower_components/angular-google-maps/dist/angular-google-maps.js" type="text/javascript"></script>
<script src="bower_components/jquery-easing/jquery.easing.min.js"></script>
<script src="bower_components/epoly-v3-bower/v3_epoly.js"></script>
OR
<script src="node_modules/angular-google-maps/dist/angular-google-maps.js" type="text/javascript"></script>
<script src="bower_components/jquery-easing/jquery.easing.min.js"></script>
```
***NOTE: epoly library is not available on node package manager, so you need to install it from bower only.

2.include required library from the CDN, Sliding marker and Marker animate. Marker animate converts all the google map marker and make it capable of sliding on google map.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/marker-animate-unobtrusive/0.2.8/vendor/markerAnimate.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/marker-animate-unobtrusive/0.2.8/SlidingMarker.min.js"></script>
```
    
3.include the files of the module in your app, as the component of the library is decoupled in different files, so we need to include all files of the module as mentioned below. 
    
```html
<script src="scripts/common/map/google-maps-animation.module.js" type="text/javascript"></script>
<script src="scripts/common/map/google-maps-animation.config.js" type="text/javascript"></script>
<script src="scripts/common/map/google-maps-animation.factory.js" type="text/javascript"></script>
<script src="scripts/common/map/google-maps-library.js" type="text/javascript"></script>
```
    
4.Now its the time to inject the dependency to your app. see reference code below.
    
```js
angular.module('myApp', ['googleMaps.module'])
```
    
5.Library has exposed all the function which are required to start animation, stop animation, adjust animation upon geting real time lat/long.

    1) create an object of googleMaps.module and initialize map.
    2) then create marker on the map for place A and for place B.
    3) then start animation.
    4) depending upon any condition, you can stop the animation and do teardown activity.

#### init google map animation:

```js
var googleMap = new googleMaps.module();

//e.g.
//googleMap.showMap(mapWrapper, options, isUnique);
googleMap.showMap(document.getElementById('map'),undefined,true);
//where in, first we need to pass element id where we want to show map
//in second param we need to pass map options
//in third param we need to pass weather we are creating new map (isUnique)

//e.g.
//googleMap.createMarker(markerOptions,isUnique);
googleMap.createMarker(markerOptions,true);
//where in, first we need to pass entire object of lat long {latitude:72,longitude:23,details:other_details}
//in second param we need to pass marker type (we are creating driver and customer marker for our app) if we want to create driver marker we will pass it as true.
```

#### execute google map animation:

```js
googleMap.startProviderAnimation();
//Function will start the animation provided both marker is set, in our case those are customer marker and driver marker.

googleMap.adjustAnimation();
//Function will adjust the animation on map, provided you are using any real time mechanism to get lat long and pass it to this service. Animation will start again for the point which is provided.

googleMap.calculateETA(srcLat, srcLgt, destinationLat, destinationLgt);
//Function will calculate and returns the google object in case of success and will return error. call to this function is optional if you want to calculate ETA and want to display it you can call it and utilize the response.
```

#### teardown google map animation:
```js
googleMap.resetMapConfig();
//reset map config variable by calling this function

googleMap.cancelTimer();
//cancel the current running animation. 
```

6.That's it -- you're done!

## More about google direction
<a target="_blank" href="https://developers.google.com/maps/documentation/directions/">Google Direction API</a>

## License

Copyright (c) 2016 Urgent.ly. http://geturgently.com
