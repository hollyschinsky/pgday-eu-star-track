---
layout: module
title: Module 4&#58; Add Searchbar Component
---

### Overview
In this step we'll add a Framework7 Searchbar component to our results page to allow the user to search/filter the results for a matching string.

## Steps
1. Begin by opening your browser and reviewing the Framework7 documentation for the `Searchbar` component at http://framework7.io/docs/searchbar.html.
1. Open `index.html` and locate the `results` template script tag:

      `<script type="text/template7" id="results">`

2. The `searchbar` needs to be placed somewhere within a `.page` class and just before a `.page-content` class. In the results template, locate the `<div>` with the `.page` class and associated `.navbar`. Insert the following search bar form which contains an input field with a clear button just after the block above and before the `<div>` with the `.page-content` class:


          <form class="searchbar">
              <div class="searchbar-input">
                  <input type="search" placeholder="Search">
                  <a href="#" class="searchbar-clear"></a>
              </div>      
          </form>

   Such as shown in the image:
<br>
<br>
  <img class="screenshot-lg" src="images/search-loc.png"/>


2. Next, open the `www/js/myApp.js` file and add the following code block just above the `myApp.onPageInit('details', function(page)` function. This function will run when the results page initializes and will initialize the searchbar component
with the parameters shown:


       myApp.onPageInit('results', function(page) {
           var mySearchbar = myApp.searchbar('.searchbar', {
               searchList: '.media-list',
               searchIn: '.item-content',
               found: '.searchbar-found',
               notFound: 'searchbar-not-found'

           })
       })   

   - `searchList` - the class selector for the list containing the data to search
   - `searchIn` - set to the class selector for the content to be searched. Defaults to `.item-title` otherwise.
   - `found` - the class selector for the element or block to display with the matches found
   - `notFound` - the class selector for the element to display in the case where no matches were found

   >See the [Framework7 docs on Pages](http://framework7.io/docs/pages.html) to learn more about the events that can be handled for a page.




3. Now go back into `www/index.html`  and add the `searchbar-found` to the `<div>` element containing the list block:

        <div class="list-block media-list searchbar-found">

4. Next add a new `<div>` element to show a message when no results are found, ensuring you specify the same class name you set in the searchbar init code. Add it just after the searchbar form.

        <div class="content-block searchbar-not-found">
               No matches found
        </div>

2. Lastly, add a div with the `searchbar-overlay` class to enable a dark overlay effect for the page content when the search bar is active. Add it just after the `searchbar-not-found` `<div>` added above.

        <div class="searchbar-overlay"></div>


### Sanity Check
The final code block with the additions should look like this:


        <form class="searchbar">
            <div class="searchbar-input">
                <input type="search" placeholder="Search">
                <a href="#" class="searchbar-clear"></a>
            </div>            
        </form>

        <div class="content-block searchbar-not-found">
               Nothing found
        </div>

        <div class="searchbar-overlay"></div>
        <div class="page-content">
          <div class="content-block-title">{{tracks.count}} tracks returned</div>
          <div class="list-block media-list list-block-search searchbar-found">
            <ul>
              {{#each tracks.items}}
                ...


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="lesson3.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="lesson5.html" class="btn btn-default pull-right">Next <i class="glyphicon
glyphicon-chevron-right"></i></a>
</div>
</div>
