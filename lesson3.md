---
layout: module
title: Module 3&#58; Detecting Offline
---

### Overview
When building for mobile you should always take an offline-first approach. There will be times when the user has no network connectivity and their experience shouldn’t suffer as a result. You can mitigate this by using local storage or another mobile database solution (SQLite, PouchDB) to provide an optimal experience in periods of low or no signal.

In this lesson you will learn how to use the Network Information plugin to detect network status. 

    $ phonegap plugin add cordova-plugin-network-information --save


[Plugin Docs](https://github.com/apache/cordova-plugin-network-information)

## Steps
1. Open `www/index.html` and add a wifi icon to the `index` page navbar on the right side to indicate the current connection status:

    #### Change this
      <!-- Top Navbar-->
      <div class="navbar">
        <div class="navbar-inner" data-page="index">
          <div class="left">
            <!--
              Left link contains only icon - additional "icon-only" class
              Additional "open-panel" class tells app to open panel when we click on this link
            -->
            <a href="#" class="link icon-only open-panel"><i class="fa fa-bars"></i></a>
          </div>
          <!-- We need cool sliding animation on title element, so we have additional "sliding" class -->
          <div class="center sliding">Search</div>
        </div>
      </div>

      #### TO
      <!-- Top Navbar-->
      <div class="navbar">
        <div class="navbar-inner" data-page="index">
          <div class="left">
            <!--
              Left link contains only icon - additional "icon-only" class
              Additional "open-panel" class tells app to open panel when we click on this link
            -->
            <a href="#" class="link icon-only open-panel"><i class="fa fa-bars"></i></a>
          </div>
          <!-- We need cool sliding animation on title element, so we have additional "sliding" class -->
          <div class="center sliding">Search</div>
          <div class="right">
            <!--
              Right icon indicates network connection               
            -->
            <a href="#" class="icon-only"><i class="fa fa-wifi"></i></a>
          </div>
        </div>
      </div>    

1. Now open the `www/js/my-app.js` file and add the following variable declaration to the top of the file under the `isIOS`
and `isMaterial` handling:

    var offline = true;

1. Now open the `www/js/my-app.js` file and add the following code to the `deviceready` function

    This code checks the status of the current connection and indicates it with the icon color (styled
    differently per platform), and then adds listeners to listen for a change in status for further handling.

    // First Check the current connection state
    if (navigator.connection && navigator.connection.type == Connection.NONE) {
      $$('.fa-wifi').addClass('color-gray');     
    }
    else {
      // It's connected, set a flag and icon colors
      offline = false;
      if (isIos) $$('.fa-wifi').addClass('color-green');
      else $$('.fa-wifi').addClass('color-white');
    }

    // Add a listener to detect a change in the connection from online to offline and vice versa
    document.addEventListener("offline", onOffline, false);
    document.addEventListener("online", onOnline, false);  

2. Add a function for the `onOffline` handler:     

        function onOffline() {
           offline = true;
           // Show a toast notification to indicate the change
           myApp.addNotification({
                title: 'Connection Status',
                message: 'A previously connected device has gone offline.'
           });
           // Set the wifi icon colors to reflect the change
           if (isIos) $$('.fa-wifi').removeClass('color-green').addClass('color-gray');
           else $$('.fa-wifi').removeClass('color-white').addClass('color-gray');            
        }

2. Add a function for the `onOnline` handler:

    function onOnline() {
        // Show a toast notification to indicate the change
        myApp.addNotification({
            title: 'Connection Status',
            message: 'A previously connected device has come back online'
        });
        // Set the wifi icon colors to reflect the change
        if (isIos) $$('.fa-wifi').removeClass('color-gray').addClass('color-green');
        else $$('.fa-wifi').removeClass('color-gray').addClass('color-white');    
        offline = false;
    }

>At this point you could further handle the experience as desired. You may want to store some data in local storage
or another on-device database to allow them to use the app with the cached data. Or save off data and sync it to a server when you're back online, just depends on the app.



<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="lesson2.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="lesson4.html" class="btn btn-default pull-right">Next <i class="glyphicon
glyphicon-chevron-right"></i></a>
</div>
</div>
