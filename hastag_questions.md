## Hashtag Quiz
##### Daniel Goldman

1. HTTP and HTTPS are two ways of sending a request from a browser to an external server. The difference between them is that an HTTPS is encrypted and thus the data in the request itself is more secure.

2. An HTTP GET request retrieves data, whereas a POST request sends out data that is already obtained to be processed (like, perhaps, saved into a database.)

3. 2xx status codes signify a success and 4xx signify a failure.

4. AJAX is a series of methods for retrieving data from server; what’s notable about AJAX is that it’s asynchronous, meaning that the rest of the code (outside of the AJAX request) will continue to run without waiting for the data to arrive. A situation where this is useful would be requesting a large image from an external server and loading it on a webpage; if this is done via AJAX, the rest of the page will continue to load and function while the image is being transferred and loaded.

5. Responsive design refers to creating CSS that reacts to changes in a webpage, particular in terms of window size. A common example is to have images shrink or disappear as a window’s size is decreased to make more room for text.

6.
```css
div {background:#fff;}  
```
Sets the background color for all HTML div tags.

```css
#div {background:#fff;}
```
Sets the background color for the HTML element with an ID of “div”.

```css
.div {background:#fff;}
```
Sets the background color for all HTML elements with a class of “div”.

7.
```html
<script src=”http://example.com/whatever.js”></script>
```
Runs the JavaScript code in the “whatever.js” file (assuming such a file exists).

```html
<script>var whatever = true</script>
```
Runs the JavaScript code written in the .html file itself; in this case the JavaScript code simply sets the variable “whatever” to the “true” Boolean.

8.
```js
var x = function(){
Return 1+1;
}();
```
This is an “iffe”; a function that is defined and then immediately invoked. The value of x is set to the value of the output of the function, which is 2.

```js
var y= function(){
Return 1+1
};
```

This is simply a function definition; the function is not invoked. The value of y is the function itself; the function can be invoked by running y().  

### Practical
1. Write HTML/CSS to draw the following scene (inline css is fine if you want):
 - One red box, 200x200 pixels
 - One blue box, 200x200 pixels
 - One green box, 100x100 pixels
 - The green box should be centered inside the red box
 - The red and blue boxes should not overlap

 ```html
 <!DOCTYPE html>
 <html lang="en">
 <head>
   <meta charset="UTF-8">
   <title>Document</title>
   <style>
   #red-box{
     position: relative;
     background-color: red;
     width: 200px;
     height: 200px;
   }

   #blue-box{
     background-color: blue;
     width: 200px;
     height: 200px;
   }

   #green-box{
     position: absolute;
     left:25%;
     top: 25%;
     background-color: green;
     width: 100px;
     height: 100px;

   }
   </style>
 </head>
 <body>
   <div id='red-box'>
     <div id= 'green-box'>
     </div>
   </div>
   <div id='blue-box'>

   </div>
 </body>
 </html>
 ```

2.
 - *Why is caching a problem for the analytics company?*
 - Once the pixel is cached by the browser, on subsequent visits to the site from that source, the pixel des not need to loaded from the customers server; it is simply retrieved from the browser cache. Thus, these subsequent visits will not get counted by the tracker.

 - *How could you prevent browser caching? (use any technique(s) you want)*
 - Browser caching can be prevented by setting the appropriate "Cache control" attribute in the HTTP request.

 - *What will happen if the customer’s website is served over HTTPS? How could you modify the tracking pixel to fix that?*
 - If the website is served over HTTPS, the pixel would need to include scripts to clear the browser's cache after the page loads.

 - *List some information the tracking company could collect (ex: IP address)*
 - Other sites visited by the user
 - Whether a user lands on an advertiser's page
 - User's IP address

 - *List some additional information information (if any) that could be collected if a script tag is used instead of an img tag.*
 - The amount of time that the user spent on the page
 - The user's interactions with the page (such as links clicked)
 - The amount it time it takes for the page to load in the user's browser.

3. Write CODE in plain javascript to do the following (jQuery is fine too, if you prefer):
Every 2 seconds:
 Check whether the image is viewable.
­ If yes, write “visible” to the console (that is, window.console).
­ If no, do nothing


```js
window.setInterval(function () {
  var $img= $('#myimage')
  var $win = $(window)

  if (  $img.position().top< $win.height()
  || ($img.position().top+$img.css(['height']) > 0)
) {
    console.log('viewable');
  }
},2000)
```
