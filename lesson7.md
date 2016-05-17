---
layout: module
title: Module 7&#58; Add Native Share Feature
---
In this module we'll learn how to share a media item with a friend through messaging, email etc using the device's native sharing features.

#### iOS
<img class="screenshot-sm" src="images/share0.png"/>
<img class="screenshot-sm" src="images/share-ios.png"/>

### Steps
Prior to this step we added a swipeout to the results view with a share button though it doesn't actually do anything yet. In this module we'll add event handling to this button to trigger the Social Sharing plugin.

>This feature requires the Social Sharing plugin and is not currently part of the PhoneGap Developer app, so to see it in
action you'll need to actually build/run with the PhoneGap CLI.

1. Open `my-app.js` and locate the page init event handler for the *list* page (`myApp.onPageInit('results')...`).
2. Add the following code to handle when a user clicks the *share* button on the swipeout. You can add it just after the  `searchbar` init handling:

        $$(page.container).find('.share').on('click', function (e) {
         var item = page.context.tracks.items[this.dataset.item]

         if (window.plugins && window.plugins.socialsharing) {
             window.plugins.socialsharing.share("Hey! I found this on Spotify. It's called " + item.name + ", check it out!",
                 'Check this out', item.album.images[2].url, item.preview_url,
                 function () {
                     console.log("Share Success")
                 },
                 function (error) {
                     console.log("Share fail " + error)
                 });
         }
         else myApp.alert("Share plugin not found");
        });


5. Try out the button now to make sure you see the share features for your native device (or a message stating the plugin is
  not supported). Remember, this is a 3rd party plugin so you can only test this feature if you're running from the CLI locally.

### Dependencies

-[Social Sharing 3rd Party Plugin](https://github.com/EddyVerbruggen/SocialSharing-PhoneGap-Plugin)

     $ phonegap plugin add cordova-plugin-x-socialsharing --save

  If you're using the CLI locally to build your app, you should add the required plugin shown above first. At the moment, the PhoneGap Developer App does not include this plugin so if you're using that to view and test the app then it will not work at this time.

  It should look something like below when you run it on iOS:

  <img class="screenshot-sm" src="images/swipeout-ios.png"/>
  <img class="screenshot-sm" src="images/share0.png"/>
  <img class="screenshot-sm" src="images/share-ios.png"/>
  <br>
  <img class="screenshot-sm" src="images/swipeout-ios.png"/>
  <img class="screenshot-sm" src="images/share0.png"/>
  <img class="screenshot-sm" src="images/share-ios.png"/>

  >The options shown in the share menu will depend on your particular devices' native sharing options.


<div class="row" style="margin-top:40px;">
 <div class="col-sm-12">
 <a href="lesson6.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
 <a href="lesson8.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
 </div>
</div>
