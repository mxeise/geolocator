<p align="center"><img width="340" height="275" src="https://raw.github.com/onury/geolocator/master/geolocator-logo.png" /><br /><br /></p>

[![CDNJS](https://img.shields.io/cdnjs/v/geolocator.svg)](https://cdnjs.com/libraries/geolocator)
[![bower](https://img.shields.io/bower/v/geolocator.svg)](https://github.com/onury/geolocator)
[![npm](http://img.shields.io/npm/v/geolocator.svg)](https://www.npmjs.com/package/geolocator)
[![release](https://img.shields.io/github/release/onury/geolocator.svg)](https://github.com/onury/geolocator)
[![Code Climate](https://codeclimate.com/github/onury/geolocator/badges/gpa.svg)](https://codeclimate.com/github/onury/geolocator)
[![dependencies](https://david-dm.org/onury/geolocator.svg)](https://david-dm.org/onury/geolocator)
[![license](http://img.shields.io/npm/l/geolocator.svg)](https://github.com/onury/geolocator/blob/master/LICENSE)
[![maintained](https://img.shields.io/maintenance/yes/2017.svg)](https://github.com/onury/geolocator/graphs/commit-activity)  

> © 2017, Onur Yıldırım ([@onury](https://github.com/onury))
> MIT License. Please see the [Disclaimer][disclaimer] and [License][license].

Geolocator.js is a utility for getting geo-location information, geocoding, address look-ups, distance & durations, timezone information and more...

## Features

 - HTML5 geolocation (by user permission) with **improved accuracy**.
 - Location by IP
 - Reverse Geocoding (address lookup)
 - Full address information (street, town, neighborhood, region, country, country code, postal code, etc...)
 - Fallback mechanism (from HTML5-geolocation to Geo-IP lookup)
 - Watch geographic position
 - Locate by mobile information
 - Get timezone information
 - Get distance matrix and duration information
 - Calculate distance between two geographic points
 - Various geographic conversion utilities
 - Get client IP
 - Fetched location includes country flag image (SVG) URL
 - Language support (depends on the service provider)
 - Supports Google Loader (loads Google APIs dynamically)
 - Dynamically create Google Maps, **on demand** (with marker, info window, auto-adjusted zoom)
 - Get static Google Map (image) URL for a location
 - Non-blocking script loading (external sources are loaded on the fly without interrupting page load)
 - No library/framework dependencies (such as jQuery, etc...)
 - Universal module (CommonJS/AMD..)
 - Small file size (9KB minified, gzipped)
 - Browser Support: IE 9+, Chrome, Safari, Firefox, Opera...

See a [**Live Demo**](https://onury.github.io/geolocator/?content=examples).

## Get Geolocator.js

Link or download via [**CDNJS**][cdnjs].  

Download full source code from [GitHub releases][releases].  

Install via **Bower**:
```
bower install geolocator
```

Install via **NPM**:
```
npm install geolocator
```

## Usage:

Example below, will attempt to get user's geo-location via HTML5 Geolocation and if user rejects, it will fallback to IP based geo-location.

Inside the `<head>` of your HTML:
```html
<script type="text/javascript" src="geolocator.min.js"></script>
<script type="text/javascript">

    geolocator.config({
        language: "en",
        google: {
            version: "3",
            key: "YOUR-GOOGLE-API-KEY"
        }
    });

    window.onload = function () {
        var options = {
            enableHighAccuracy: true,
            timeout: 5000,
            maximumWait: 10000,     // max wait time for desired accuracy
            maximumAge: 0,          // disable cache
            desiredAccuracy: 30,    // meters
            fallbackToIP: true,     // fallback to IP if Geolocation fails or rejected
            addressLookup: true,    // requires Google API key if true
            timezone: true,         // requires Google API key if true
            map: "map-canvas",      // interactive map element id (or options object)
            staticMap: true         // map image URL (boolean or options object)
        };
        geolocator.locate(options, function (err, location) {
            if (err) return console.log(err);
            console.log(location);
        });
    };

</script>
```

If you've enabled `map` option; include the following, inside the `<body>` of your HTML:
```html
<div id="map-canvas" style="width:600px;height:400px"></div>
```
Read [**API documentation**][api-docs] for lots of other features and examples.

## Important Notes

- Since Geolocation API is an HTML5 feature, make sure your `doctype` is HTML5 (e.g. `<!DOCTYPE html>`).
- Make sure you're calling Geolocation APIs (such as `geolocator.locate()` and `geolocator.watch()`) from a secure origin (i.e. an **HTTPS** page). In Chrome 50, Geolocation API is [removed][chrome-unsecure] from **unsecured origins**. Other browsers are expected to follow.
- Although some calls might work without a key, it is generally required by most Google APIs (such as Time Zone API). To get a free (or premium) key, [click here][google-docs]. After getting a key, you can enable multiple APIs for it. Make sure you [enable][google-console] all the APIs supported by Geolocator. *(If you don't have a key, you can still use Geolocator like the previous versions, but with limited features.)*
- Geolocator now supports a single Geo-IP provider, FreeGeoIP. You can use `geolcoator.setGeoIPSource()` method to set a different Geo-IP source.
- <strike>On Firefox, callback is not fired for Geolocation, if user clicks "Not Now" instead of "Never".</strike> This is now fixed in Firefox version 53 with the new permission prompt redesign. (See bugzilla [675533][bug-675533].)

## Under the Hood

Geolocator v2 is written in ES2015 (ES6), compiled with [Babel][babel], bundled with [Webpack][webpack] and documented with [Docma][docma].

## Change Log

See version changes [here][changelog].

## License

MIT. See the [Disclaimer][disclaimer] and [License][license].


[api-docs]:https://onury.github.io/geolocator/?api=geolocator
[changelog]:https://onury.github.io/geolocator/?content=changelog
[license]: https://github.com/onury/geolocator/blob/master/LICENSE
[disclaimer]: https://github.com/onury/geolocator/blob/master/DISCLAIMER
[uncompressed]: https://raw.github.com/onury/geolocator/master/src/geolocator.js
[compressed]: https://raw.github.com/onury/geolocator/master/src/geolocator.min.js
[cdnjs]:https://cdnjs.com/libraries/geolocator
[demo]: http://rawgit.com/onury/geolocator/master/example/index.html
[example-img]: https://raw.github.com/onury/geolocator/master/screenshots/geolocator-example.jpg
[npm-package]: https://www.npmjs.com/package/geolocator
[releases]:https://github.com/onury/geolocator/releases
[legacy-version]:https://github.com/onury/geolocator/releases/tag/v1.2.9
[babel]:https://github.com/babel/babel
[webpack]:https://github.com/webpack/webpack
[docma]:https://github.com/onury/docma
[google-docs]:https://developers.google.com/maps/documentation/javascript
[google-console]:https://console.developers.google.com
[chrome-unsecure]:https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only?hl=en
[bug-884921]:https://bugzilla.mozilla.org/show_bug.cgi?id=884921
[bug-675533]:https://bugzilla.mozilla.org/show_bug.cgi?id=675533
