## How To Track User's Location

Hello everyone 👋

In this article, we will see how can we get access to the user's location on our website.

Tracking the user's location is not always necessary, but if you are building something like a location sharing application, a map-related application or to offer customized results based on the user's location then you need access to the user's location. By application, I mean web-based applications.

So how can we get access to the user's location? 

Modern browsers provide almost everything we need in our application to enhance the user's experience. And here comes the `Geolocation API` which is a Web API provided by the browsers to get access to the user's location with their consent.

Live link to try it out at the end of the article.

### What is Geolocation API?

`Geolocation API` is a Web API that gives Web content access to the location of the device.

> Permission required to use the `Geolocation API`.

### Implementation 📍

Let's understand the implementation of the API.

We can access the API from the browser's `window.navigator` object.

#### Check For `Geolocation API` Support

```javascript
if (Boolean(window.navigator.geolocation)) {
  // It supports
  ...
}
```

### Geolocation Interface 🗺️

`geolocation` is the main method that we need to access to get, track, cancel tracking the location. It has three properties (methods):

- `getCurrentPosition`
- `watchPosition`
- `clearWatch`


### Current Location 📌

To get the current location of the device, we will use the `getCurrentPosition` method. This method will pass the current `position` to the `positionCallback` and in case of `error`, it will pass the `error` object to the `errorCallback`.

```javascript
window.navigator.geolocation.getCurrentPosition(
    positionCallback,
    errorCallback
);
```

#### Position Callback

```javascript
function positionCallback(position) {
  // Assigning coords object for easier access.
  const coords = position.coords;

  // Position of the longitude .
  const longitude = coords.longitude;

  // Position of the latitude.
  const latitude = coords.latitude;

  // Accuracy of latitude & longitude in meters.
  const accuracy = coords.accuracy;

  // Altitude in meters, relative to sea level.
  const altitude = coords.altitude;

  // Accuracy of the altitude in meters. Value can be null.
  const altitudeAccuracy = coords.altitudeAccuracy;

  // Direction towards which the device is facing. This value specified
  // in degrees clockwise from North. Value can be null.
  const heading = coords.heading;

  // The velocity of the device in m/s. Value can be null.
  const speed = coords.speed;

  // The time at which the location was retrieved.
  const time = position.timestamp;
}
```

All the values are of the `double` type.

#### Error Callback

```javascript
function errorCallback(err) {
  let msg;
  switch (err.code) {
	case err.PERMISSION_DENIED:
		msg = "User denied the request for Geolocation.";
		break;
	case err.POSITION_UNAVAILABLE:
		msg = "Location information is unavailable.";
		break;
	case err.TIMEOUT:
		msg = "The request to get user location timed out.";
		break;
	case err.UNKNOWN_ERROR:
		msg = "An unknown error occurred.";
		break;
  }
}
```

I think this function is very self-explanatory. It is just comparing the error code with the error type and we can handle it in any way.

### Live Location 🌎

To track the live location of the device we can call the `watchPosition` method. This method takes the same arguments as `getCurrentPosition`. The method will pass the updated current `position` to the `positionCallback` as the device change its location and in case of `error`, it will pass the `error` object to the `errorCallback`.

```javascript
const id = window.navigator.geolocation.watchPosition(
   positionCallback,
   errorCallback
);
```

- `watchPosition` method returns an `id` which we can use to stop tracking.

### Stop Tracking  🛑

To stop tracking the live location we can call the `clearWatch` method. The method expects `id` as an argument.

```javascript
window.navigator.geolocation.clearWatch(id);
```

### Example✨

Check out the [GitHub repo](https://github.com/bibekkakati/blogs-projects/tree/main/web/geolocation-api) for sample code.

Try it out [here](https://bibekkakati.github.io/blogs-projects/web/geolocation-api/index.html).

*`Mobile devices will give more accuracy.`*

___

Enjoyed? Give it a thumbs-up 👍

Thank you for reading | Feel free to [connect](https://bibekkakati.me) 👋