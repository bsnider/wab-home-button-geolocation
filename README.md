# wab-home-button-geolocation
This Web AppBuilder for ArcGIS widget is a modification of the stock home button widget.  On app load, the widget will use the Geolocation Web API to zoom to the user's location.


## Features

* Zoom to a user's location using the [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/getCurrentPosition) on Home Widget load (essentially app load)
* Sets the Home Button's extent to the user's location
* If user denies access to geolocation services, the extent for the Home Button defaults to the app's config file


## Relevant Code
```javascript
// Use browser geolocation to obtain user's coords
if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(lang.hitch(this, success), lang.hitch(this, error));
} else {
  console.log("Geolocation is not supported by this browser.");
  lang.hitch(this, error);
}

function success(position) {
  console.log("Latitude: " + position.coords.latitude + ", Longitude: " + position.coords.longitude);
  // home button widget requires an extent.  Must convert coords to extent
  var expandDelta = .1
  var ptExtent = new Extent(
    position.coords.longitude - expandDelta,
    position.coords.latitude - expandDelta,
    position.coords.longitude + expandDelta,
    position.coords.latitude + expandDelta,
    new SpatialReference(4326)
  );
  this.createHomeDijit({
    map: this.map,
    extent: ptExtent
  });
  this.map.setExtent(ptExtent);
}
```


## Requirements

* Notepad or your favorite HTML editor
* Web browser with access to the Internet
* Only tested with WAB 2.5


## Installation Instructions

* Fork and then clone the repo or download the .zip file.


## Resources

* [LinkedIn](https://www.linkedin.com/in/bradleysnider/)
* [GitHub](https://github.com/bsnider)
* [Twitter](https://twitter.com/bjsnider)
* [Website](http://bradleyjsnider.com)
* [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/getCurrentPosition)
* [Web appBuilder for ArcGIS (Developer Edition)](https://developers.arcgis.com/web-appbuilder)


## Issues

Find a bug or want to request a new feature?  Please let us know by submitting an issue.


## Contributing

Anyone and everyone is welcome to contribute.
