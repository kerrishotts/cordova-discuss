#FAQ

### Do cookies work in Cordova apps?

The rules for cookies in the Cordova apps are the same as desktop browsers. You should _not_ expect your app to persist cookies for its own use, because Cordova applications aren't usually backed by a web server and so have no place to store cookies. Most Cordova platforms serve files from the `file:///` protocol, and are subject to standard browser security rules. Non-GET requests whould be subject to CORS and preflight OPTIONS request would be issued for POST and other verbs. Good explanations about CORS and Cordova app can be found [here] (http://stackoverflow.com/questions/9103876/cors-cookie-credentials-from-mobile-webview-loaded-locally-with-file). In case you haven't heard about CORS, [CORS on HTML5Rocks](http://www.html5rocks.com/en/tutorials/cors/) is a good resource.

### How to work with cookies in Cordova apps?

There are two ways in which you may want to use cookies. The first by using `XMLHttpRequest` (XHR / AJAX) to request remote resources. Unless you specifically remove them, your Ajax library will automatically use cookies in subsequent calls to remote APIs and resources you request. So if some API returns a cookie required for future calls, you can assume it will be automatically sent when your app hits it again.

The other way your app may desire to use cookies is locally - ie within the app itself. This does not make sense within a Cordova app as it usually isn't running on a proper web server itself. If your intent is simply to store data for the app then you should make use the various [existing local storage methods](http://cordova.apache.org/docs/en/4.0.0/cordova_storage_storage.md.html#Storage).

