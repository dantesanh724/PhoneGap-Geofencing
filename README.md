PhoneGap-Geofencing
===================

Geofencing And Significant Location Change Monitoring Plugin For PhoneGap.

This Phonegap Plugin has been developed by AnGe724.  
Feel free to use the code in any projects according the the license at the bottom of this readme.

I am happy to offer my consulting services if needed and can be contacted at: edmondan724@gmail.com

## DESCRIPTION ##

* This plugin provides a simple way to use iOS and Android Region Monitoring in PhoneGap applications.
* Significant location changes API is exposed.
* Simple JS interface is exposed to allow the adding and removing of regions to monitor.
* Included ability to receive realtime region notifications when regions are entered and exited.

## WHAT IS GEOFENCING ##

Geofencing is a way to monitor geographic regions.  
In iOS it allows an app to be informed when a specified geographic region is entered or exited.

## Installation
The plugin can either be installed into the local development environment or cloud based through [PhoneGap Build][PGB].

### Adding the Plugin to your project
Through the [Command-line Interface][CLI]:
```bash
# ~~ from master ~~
cordova plugin add https://github.com/dantesanh724/PhoneGap-Geofencing.git && cordova prepare
```

### Removing the Plugin from your project
Through the [Command-line Interface][CLI]:
```bash
cordova plugin rm com.anh724.cordova.plugin.geofencing
```

## INCLUDED FUNTIONS ##

DGGeofencing.js contains the following functions:

1. initCallbackForRegionMonitoring - Initializes the PhoneGap Plugin callback.  
2. startMonitoringRegion - Starts monitoring a region.
3. stopMonitoringRegion - Clears an existing region from being monitored.
4. startMonitoringSignificantLocationChanges - Starts monitoring significant location changes.
5. stopMonitoringSignificantLocationChanges - Stops monitoring significant location changes.

## PLUGIN CODE EXAMPLE ##

To add a new region to be monitored use the DGGeofencing startMonitoringRegion function.
The parameters are:

1. fid - String - This is a unique identifier.
2. latitude - String - latitude of the region.
3. longitude - String - latitude of the region.
4. radius - Integer - Specifies the radius in meters of the region.

Example:
	
	var params = [location.id, location.location.lat, location.location.lng, "10"];
	DGGeofencing.startMonitoringRegion(params, function(result) {}, function(error) {
		alert("failed to add region");
	});

To remove an existing region use the DGGeofencing removeRegion function.
The parameters are:
1. fid - String - This is a unique identifier.
2. latitude - String - latitude of the region.
3. longitude - String - latitude of the region.

Example:

	var params = [item.fid, item.latitude, item.longitude];
	DGGeofencing.stopMonitoringRegion(params, 
	function(result) {

		// not used.

	}, function(error) {
		// not used
	});


To start monitoring signifaction location changes use the DGGeofencing startMonitoringSignificantLocationChanges function.
No parameters.

Example:

	DGGeofencing.startMonitoringSignificantLocationChanges(
		function(result) { 
			console.log("Location Monitor Success: " + result);				   
		},
		function(error) {  
			console.log("failed to monitor location changes");   
		}
	);

To start monitoring signifaction location changes use the DGGeofencing startMonitoringSignificantLocationChanges function.
No parameters.

Example:

	DGGeofencing.stopMonitoringSignificantLocationChanges(
		function(result) { 
			console.log("Stop Location Monitor Success: " + result);				   
		},
		function(error) {  
			console.log("failed to stop monitor location changes");   
		}
	);
	
## HOW TO SETUP REGION AND LOCATION NOTIFICATIONS ##

Of course adding and removing monitored regions would be useless without the ability to receive real time notifications when region boundries are crossed.
This setup will allow the JavaScript to receive updates both when the app is running and not running.

Example:

```
// gets called when region monitoring event is submitted from iOS, Android
function processRegionMonitorCallback (result) {
    var callbacktype = result.callbacktype;

    if (callbacktype == "initmonitor") {

    } else if (callbacktype == "locationupdate") {

    	var fid = result.regionId;
		
		var new_timestamp = result.new_timestamp;
		var new_speed = result.new_speed;
		var new_course = result.new_course;
		var new_verticalAccuracy = result.new_verticalAccuracy;
		var new_horizontalAccuracy = result.new_horizontalAccuracy;
		var new_altitude = result.new_altitude;
		var new_latitude = result.new_latitude;
		var new_longitude = result.new_longitude;

		var old_timestamp = result.old_timestamp;
		var old_speed = result.old_speed;
		var old_course = result.old_course;
		var old_verticalAccuracy = result.old_verticalAccuracy;
		var old_horizontalAccuracy = result.old_horizontalAccuracy;
		var old_altitude = result.old_altitude;
		var old_latitude = result.old_latitude;
		var old_longitude = result.old_longitude;

    } else if (callbacktype == "monitorremoved") {

    } else if (callbacktype == "monitorfail") {

    } else if (callbacktype == "monitorstart") {

    } else if (callbacktype == "enter") {

    	//result.callbacktype
       	//result.regionId
       	//result.message
       	//result.timestamp

    } else if (callbacktype == "exit") {

       	//result.callbacktype
       	//result.regionId
       	//result.message
       	//result.timestamp

    }
}

// setup 1 region for monitoring on deviceready
function onDeviceReady () {

    window.plugins.DGGeofencing.initCallbackForRegionMonitoring(new Array(), processRegionMonitorCallback, function(error) {
        console.log("init error");
    });

    var params = [1, 40.781552, -73.967171, "150"];
    window.plugins.DGGeofencing.startMonitoringRegion(params, function(result) { console.log('watching');}, function(error) {
        console.log("failed to add region");
    });

}

document.addEventListener("deviceready", onDeviceReady, false);
```


## LICENSE ##

Copyright (c) 2014 Dov Goldberg

EMAIL: edmondan724@gmail.com   

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

[cordova]: https://cordova.apache.org
[PGB_plugin]: https://build.phonegap.com/plugins/413
[CLI]: http://cordova.apache.org/docs/en/3.0.0/guide_cli_index.md.html#The%20Command-line%20Interface
[PGB]: http://docs.build.phonegap.com/en_US/3.3.0/index.html
[apache2_license]: http://opensource.org/licenses/Apache-2.0
