# PixelsJS Documentation

Pixels.JS is an image filtering library with over 70 photo filters for use in the browser or with Node.JS.

Image filtering comprises vintage filters, solarizers, inverters, and over seventy more.
The photo filters span a variety of genres including vintage, retro, and tinted-themed 
filters. 

To find filters based on a certain category,
then just check for our Category specific pages, which list each of the filters. 

## Importing Pixels.JS
### In-Browser
Include the following script tag in your page's head tag: 

```html
<script src="https://cdn.jsdelivr.net/gh/silvia-odwyer/pixels.js@0.8.1/dist/Pixels.js"></script>
``` 

### Node.JS
Library not yet deployed as a package to NPM.
[coming soon]

## Using Pixels.JS
### Browser
##### HTML
After you've included a copy of Pixels.JS in your head tag, include an image in your HTML:
```html
<img src="image.PNG" id="img"/> 
```

##### Javascript
Then, in your JavaScript:
```javascript
// Select the image you wish to filter
var img = document.getElementById("img")

// First parameter is the image object, and the second is the filter you wish to apply.
img.onload = function() {
  pixelsJS.filterImg(img, "twenties");      
}
```

#### Node.JS
Usage for Node.JS varies slightly to the browser. Whereas in-browser Pixels.JS automatically replaces the image on the webpage with the newly filtered one, 
in Node, your environment and canvas libraries can differ, so we've kept usage flexible for Node. 

This example uses node-canvas and get-image-data, two NPM modules that make canvas rendering easier, however, you can choose whatever libraries you like; this example merely illustrates using Pixels.js in tandem with node-canvas. 

```javascript
const get_image_data = require('get-image-data');
const PixelsJS = require("pixelsjs");
const Canvas = require('canvas')

var canvas = new Canvas(200, 200),
    ctx = canvas.getContext('2d'),

get_image_data('./image.jpg', function(error, info) {
  var imgData = info.data
  
  let newImgData = PixelsJS.filterImgData(imgData, "solange");
  
  ctx.putImageData(imgData, 0, 0);
  
})
```

## Step-By-Step Guide
You can quickly get started with Pixels.JS using the sample code above, but if you're new to web development or want a guided tour, 
just check out the guides below. 

### Browser
1. Include the image on the webpage. `<img src="path/to/image.PNG" id="img">`

2. In your JS, select the image you want to add filters to, by selecting the unique ID name of the image. `var img = document.getElementById("img")`

3. Pass the image into the filter function, and include the name of the filter you want. 
`var filtered_img = Pixels.JS.filterImg(img, "sepia")`

The method filters the image and replaces the current image with the filtered one, so there's no need to append the new image to the DOM, as this is already
done for you. 

### Node.JS
Simply get the image data of the image and pass it to the filterImgData function. The output will be the new image data. 
You can then place this new image data onto your canvas.

## Filter Categories
### Offset Filters
These selection of filters produce a distinct RGB offset, at a specific location. If the offset is marked with extreme in its filter name,
then it the offset is 35 pixels or greater.
Double offset filters consist of two offsets applied, one in each direction, and can consist of a multitude of colours, depending on the filter applied.

Offset filters add a futuristic, technological, almost reminiscient of 3D filters feel to any image.

### Tinted Filters
These filters add or subtract the amount of "red", "blue", or "green" in each pixel, thus adding a slight tint or hue to the image. Perhaps these filters
are most common in photography apps such as Instagram and Snapchat, and are best suited towards those who would like tp
add a warmer or cooler glow to an image. This usually involves adding or subtracting a fixed constant from the amount of red, blue, or green in each pixel.
Pixels.JS accommodates this by including more than thirty tinted filters in our collection.

### Vintage Filters
These filters include greyscale, duoscale, and sepia filters. They involve getting the average of the red, blue, and green data per pixel
and then adding or subtracting a constant to that number. 

### Noise Generators 
Noise generators add a random amount of red, green, or blue to each pixel's value or by multiplying the R, G, and B values of a pixel 
by a random number. 
Images are also tinted to create noise generation with a certain tint, such as purple noise generation, and so forth. 

### Brightness Adjustments
By adding a fixed constant to the R, G, and B values of each pixel, the brightness of an image can be increased, and subtraction will result in darkening an image.

## Methods
PixelsJS contains three key methods:

- filterImg 

- filterImgData

- getFilterList

## filterImg(imageObject, filterName) -> canvas
*In-Browser Only*

This method takes an image object and a filter name, and it returns the filtered image as a canvas.
The original image is replaced with the filtered image in canvas format. 
The list of filternames can be seen in the Filters List below.
### Parameters
1. imageObject: This consists of a HTML Image Element. If you add an image to the webpage, and select it with getElementById or querySelector, 
this is the object you then pass to the filterImg method.
2. filterName: Name of the filter you'd like. If the filter is invalid, an error will be thrown.

### Returns
A canvas object. The original image is automatically replaced by the new canvas.

## filterImgData(imgData, filter) -> imgData
Every image consists of pixels, whose pixel data can be retrieved using the getImageData method, as found in the HTML5 Canvas API. 

```javascript
    let imgData = context.getImageData(0, 0, canvas.width, canvas.height);
```

If you'd like to filter only the image data or work with the image data alone (and not the image), you can use this method instead. 
It filters or manipulates the image data passed to it, and then returns the filtered image data object.
You can then place this image data on a canvas or replace the current image data with this data. 

```javascript
    context.putImageData(newImgData, 0, 0)
```

### Parameters
1. imgData: This consists of an image data ndArray, as taken from the image by using the getImageData method on the image. 
2. filterName: Name of the filter you'd like. If the filter is invalid, an error will be thrown.

### Returns
The filtered image data. 

## getFilterList() -> array
To get a list of all filters available in PixelJS, just call getFilterList.

An array of all filters will be returned.

## Complete Example
### Browser
```javascript
    let canvas = document.querySelector("canvas");
    let context = canvas.getContext("2d")

    // Get the image data found within the canvas
    let imgData = context.getImageData(0, 0, canvas.width, canvas.height);

    // Filter the image data
    let newImgData = PixelsJS.filterImgData(imgData, "solange");

    // Replace the old image data with the new image data.
    context.putImageData(newImgData, 0, 0);
```

### NodeJS
```javascript
const get-image-data = require('get-image-data');
const Pixels.JS = require("Pixels.JS");
const Canvas = require('canvas')

var canvas = new Canvas(200, 200),
    ctx = canvas.getContext('2d'),

get-image-data('./image.jpg', function(error, info) {
  var imgData = info.data
  
  let newImgData = PixelsJS.filterImgData(imgData, "solange");
  
  ctx.putImageData(imgData, 0, 0);
  
})
```

## All Filters
A complete Demo of all filters, along with their names, can be found at [PixelsJS' official website](https://silvia-odwyer.github.io/pixels.js/) 
under the Demo section. 

## Accompanying Web App
An accompanying web app is also provided to test out each of the image filters. You can make use of the [web app here](https://silvia-odwyer.github.io/pixels.js/demo).

## Contact
The documentation and code is maintained by Silvia O'Dwyer ( silviaodwyerdev [at] gmail dot com). For improvements to the documentation or code, 
you can make a Pull Request on GitHub or open an Issue. You can also contact me via the email provided above. 