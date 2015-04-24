#FAQ

## Sections

* [Cookies](#cookies)
* [Design](#design)
* [Miscellaneous](#misc)

## [Cookies](id:cookies)

### Do cookies work in Cordova apps?

The rules for cookies in the Cordova apps are the same as desktop browsers. You should _not_ expect your app to persist cookies for its own use, because Cordova applications aren't usually backed by a web server and so have no place to store cookies. Most Cordova platforms serve files from the `file:///` protocol, and are subject to standard browser security rules. Non-GET requests whould be subject to CORS and preflight OPTIONS request would be issued for POST and other verbs. Good explanations about CORS and Cordova app can be found [here] (http://stackoverflow.com/questions/9103876/cors-cookie-credentials-from-mobile-webview-loaded-locally-with-file). In case you haven't heard about CORS, [CORS on HTML5Rocks](http://www.html5rocks.com/en/tutorials/cors/) is a good resource.

### How to work with cookies in Cordova apps?

There are two ways in which you may want to use cookies. The first by using `XMLHttpRequest` (XHR / AJAX) to request remote resources. Unless you specifically remove them, your Ajax library will automatically use cookies in subsequent calls to remote APIs and resources you request. So if some API returns a cookie required for future calls, you can assume it will be automatically sent when your app hits it again.

The other way your app may desire to use cookies is locally - ie within the app itself. This does not make sense within a Cordova app as it usually isn't running on a proper web server itself. If your intent is simply to store data for the app then you should make use the various [existing local storage methods](http://cordova.apache.org/docs/en/4.0.0/cordova_storage_storage.md.html#Storage).

## [Design](id:design)

### How do I make my app fit different screen sizes and resolutions?

Here are some tips and useful resources that should help you create apps that can respond to the various screen sizes and resolutions that are out there:

 * Avoid fixed heights and widths when possible.
 * Use percentages when possible.
 * Take advantage of typographical CSS units like `em` and `rem` ([Compatibility](http://caniuse.com/#feat=rem)) and viewport units like `vh`, `vw`, `vmax`, and `vmin` ([Compatibility](http://caniuse.com/#feat=viewport-units)).
 * Use relative and absolute positioning to anchor to containing elements when necessary.
 * Use the (relatively new) Flexible Box Layout Module ([Compatibility](http://caniuse.com/#feat=flexbox)) for complex layouts.
 * Don't just _scale your layout up or down_ -- think about how your user interface should work on screens of different sizes.
 * Use [Media Queries](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries) to detect pixel density, screen width and height, orientation, and other useful information.

These techniques fall under the term "responsive design". The idea here is that your app should _respond_ to the device's capabilities and render itself appropriately. For more information about Responsive Design, check out these resources:

 * [Wikipedia Article](http://en.wikipedia.org/wiki/Responsive_web_design)
 * [A List Apart's articles on Responsive Design](http://alistapart.com/topic/responsive-design)

### How do I make my images fit different screen sizes and resolutions?

When designing your images, you should plan _in advance_ that they will need to be rendered on devices with differing resolutions, aspect rations, and pixel densities. If you know in advance that the full-screen background image that you are designing will need to cover a wide variety of screens, you can design it appropriately to fit for a large number of scenarios. Alternatively, there may be no other way around the different dimensions but to make different versions of the image.

Here are some tips to help make responsive images easier to deal with:

 * Build your artwork using a vector editor. If you are using photographs, _start_ with the highest possible resolution image available.
 * Use [`background-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size) where appropriate. For example, you can set an image to fit within an element while maintaining its aspect ratio by using `contain`, or you can allow an image to fill the available space (again while maintaining the aspect ratio) by using `cover`. These two property values are very useful for background and heading images. You can also use `background-size` to scale an image to specific dimensions using the various CSS units.
 * _Avoid_ scaling a lot of images when you can avoid it. This conflics a little with the prior bullet. Scaling will introduce visual artifacts (such as blurriness) and also impacts rendering performance. For example, you shouldn't attempt to scale a 20 megapixel photograph down to a 25 kilopixel thumbnail using HTML and CSS. Instead, render the thumbnail(s) you need in advance. 
 * Provide images for each pixel density you wish to support. For iOS, this means providing @1x (low DPI), @2x (Retina), and @3x (Retina HD) assets. For photographs, these are usually just pre-rendered versions of the original image. For vector images, they the image may need to be tweaked to look its best at each pixel density. For Android and other platforms, there are many more pixel densities in use, and they may even be fractional. Target those densities that make sense for your app and your target audience.
 * Avoid text in your images as much as possible -- the differences between how your image editor renders (and scales) text will be very obvious when compared against text in the rest of your app. Blurry text in an image or icon will be immediately obvious.

## [Miscellaneous](id:misc)

### Can I use PHP / ASP.Net / etc.?

Cordova serves all your app's assets from the device's file system without any processing. This means that PHP, ASP.Net, and other languages that require interpretation, processing, compilation, etc. will not work. If you need to use these technologies, you'll need to implement a remote web service on a server that you control that your application can call at the appropriate times.

### Can I use (insert CSS/HTML/JS feature here)?

Here are some great resources for determining feature compatibility and availability:

 * [Can I use](http://caniuse.com)
 * [Kangax's EcmaScript Compatibility Tables](http://kangax.github.io/compat-table/)

