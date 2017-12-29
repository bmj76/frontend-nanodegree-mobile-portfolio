# frontend-nanodegree-website-optimization by Brian Johnson

Working on increasing the Google PageSpeed insights score and the scrolling FPS on an existing page.

## Getting Started
Load any Web Server on your PC, then clone the repository under the webroot 
folder (ie. htdocs) to an weboptimization folder.  Example:

`git clone https://github.com/bmj76/frontend-nanodegree-mobile-portfolio.git c:\miniweb\htdocs\weboptimization`

Simply open http://127.0.0.1:8000/weboptimization/index.html to start the app.

To view the Google PageSpeed score, you will also need to clone this to a server reachable on the Internet or use a pinhole application such as ngrok.

## Improvements Made

### Removed render blocking

CSS WebFont - I used a suggestion from https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery to inline css even when it is contained in a separate file.

CSS - Moved the style.css content into a `<style>` tag within index.html.  I considered not making this change because other html files on the page use the same CSS file, but it is short enough so I went for it in the name of a faster load time.

CSS - I added a media statement to the print.css tag.  This file is only needed if the page is being printed.  Adding this removes it as a render blocking CSS file in the CRP.

JavaScript - I was able to add the async keyword to the call to Google analytics.  This is not necessary in the CRP.

### Minified Code

All local Javascript and CSS have been minified (that are loaded by index.html).  I did not apply the same CRP improvements to the Pizza page..  

I did also Minify the HTML, but found that it only improved the page load slightly.  (1 point gain on mobile pagespeed, 0 point gain on desktop) I decided not to minify it in the final project in favor of better readability.

### Image Resizing

All images have been compressed using http://Compressor.io and where necessary resized using ImageMagick.

### Performance Improvements to the Pizza page scrolling

Moved the `var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;` line outside of the for loop to avoid having to recalculate style over 200 times per function call.  This was the biggest cause of Jank.

Discovered that there are 200 floating pizzas on the page.  Not all need to have the moving effect applied because they are not visible.  I divided by 7 to apply the effect to only the first ~28 or so.  Obviously it would be best not to create 200, but I'm not sure what other code would need to change at this time to accomplish that.  

### Performance Improvements to the Pizza Size Slider

Refactored the changePizzaSizes function to use a simpler method to adjust size using % instead of a more complicated pixel size based on screen width.

``` // Based on size, set a % to use
    switch(size) {
      case "1":
        pizzaSize = 25.00;
        break;
      case "2":
        pizzaSize = 33.33;
        break;
      case "3":
        pizzaSize = 50.00;
        break;
      default:
        pizzaSize = 25.00;
    }

    var allPizzas = document.querySelectorAll(".randomPizzaContainer");

    for (var i = 0; i < allPizzas.length; i++) {
      allPizzas[i].style.width = pizzaSize + '%';
    }```






 
