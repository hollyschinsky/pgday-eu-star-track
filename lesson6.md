---
layout: module
title: Module 8&#58; Add Swipeout Handling
---

### Overview
In this step we'll add a common mobile UX feature to our app to make it more useful; swipeouts. Swipeouts
allow you to swipe left or right over list elements to reveal further actions.

The iOS Reminders app is a good example of an app using swipeouts:

   <img class="screenshot-lg-center" src="images/remind2.png"/>

## Steps
1. Take a moment to review the [Framework7 Swipeout Docs](http://framework7.io/docs/swipeout.html)
1. Open `index.html` and add the `swipeout` class to the current `<li>` tag
      <li class="swipeout">

2. Now add a new `<div>` element with the class of `swipeout-content` just below it the `<li>`
and end it after the <`li`>

      <div class="swipeout-content">

2. Add the following snippet just before the closing `<\li>`. This code will create the action itself
with a link containing a `share` class that we'll list to for clicks and pass along the index of the
item clicked. It also sets the share icon based on the platform.

                <!-- Swipeout actions right -->                
                <div class="swipeout-actions-right">
                    <!-- Swipeout actions links/buttons -->
                    <a href="#" class="share" data-item="{{@index}}">
                    {{#if @global.material}}
                        <i class="icon fa fa-share-alt fa-3x"></i></a>
                    {{else}}
                        <i class="icon fa fa-share fa-3x"></i></a>
                    {{/if}}                      
                </div>




      {% raw %}

     {% endraw %}

2. In the above definition we have buttons in the `swipeout-actions-right` and `swipeout-actions-left` that require some handlers to invoke code to actually do something when clicked. In this
step we will add the handling for them.

   >The {% raw %}`data-item="{{@index}}"`{% endraw %} syntax will pass the index of the item clicked on so we can then reference the right item in the code.  

3. Add a Page Init handler to use for setting up events we want to handle on the list page specifically.

        myApp.onPageInit('list', function (page) {

        });'

4. **Add Favorites Handler** - the `star` button indicates that the user can add this item as a favorite. Open `my-app.js` and add the following into the list page
 init handler created in the previous step `myApp.onPageInit('list', function (page) {...`

        $$(page.container).find('.favorite').on('click', function (e) {
            var item = page.context[this.dataset.item]; //this.dataset.item returns data held in data-item attribute set in template
            myApp.alert(item.name + ' added to favorites!');
        });

   >Note the use of the `page.context[this.dataset.item];` As mentioned above, we passed the index of the current item clicked on the `data-item` attribute. Here
   we use it to retrieve that index from the page context. The page context is the array of results we received and supplied for the list template.


5. **Add Preview Handler** - the left swipeout `play` button indicates the user can click it to play a preview of this item. Open`my-app.js` and add the following into
the list page init handler as well:

        $$(page.container).find('.preview').on('click', function (e) {
            var item = page.context[this.dataset.item]; //this.dataset.item returns data held in data-item attribute set in template

            myApp.alert("Previewing " + item.name);
            var media = new Media(item.preview_url, function () {console.log("Media Success");},function (error)
                {console.log("Media fail " + error)},null);
            media.play();
            setTimeout(function() {media.stop()},7000) //preview for 7 seconds
        });

### Dependencies
  The preview feature above requires the Media Plugin. If you're testing with the PhoneGap Developer app on your mobile device, then it's already
  configured for you in the sandboxed environment. If you're running locally with the CLI however, be sure to add the plugin.

   - [Media Plugin](https://github.com/apache/cordova-plugin-media)

            $ phonegap plugin add cordova-plugin-media --save

  >This command will also add the Cordova File Plugin by default since it's a required dependency.

6. You may notice there's also a `Share` swipeout button but we will be handling that in a later module since it requires a 3rd party plugin.

7. Run the app to make sure you see the click events firing when you tap on the Preview and Favorites buttons in the swipeouts.

  >Based on the F7 docs, the swipeout support will not work well in the browser so you should test this feature via the PhoneGap Developer App or the CLI locally.

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="lesson6.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="lesson9.html" class="btn btn-default pull-right">Next <i class="glyphicon
glyphicon-chevron-right"></i></a>
</div>
</div>
