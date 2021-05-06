## How To Use Vibration API in Your Website

Hello everyone 👋

In this article, we will see how can we use `Vibration API` in our websites.

We can use the `Vibration API` to provide haptic or vibration feedback to the user using the website for their actions.

Most modern mobile devices include vibration hardware, which lets software code provide physical feedback to the user by causing the device to shake. So this API works well with mobile devices only and targeted for the same.

The `Vibration API` allows the web apps to access the vibration hardware if it exists.


### Implementation 👨‍💻

Let's explore the API.

We can access the API from the browser's `window.navigator` object.

#### Check `Vibration API` Support

It is always a good idea to check for API support.

```javascript
if (Boolean(window.navigator.vibrate)) {
	// It Supports
	...
}
```
- `vibrate` is a method that is responsible for the vibration.
- It expects one argument.

> Argument is a number or an array of numbers for a series of vibrations. Those numbers are considered as `milliseconds`.

If the method was unable to vibrate because of invalid parameters, it will return `false` else it returns `true`.

#### Single Vibration  📳

For a single vibration, we can pass a single number directly or in an array.

```javascript
// Will vibrate the device for 500ms
window.navigator.vibrate(500);

// Same as the above line
window.navigator.vibrate([500]);
```

#### Pattern Vibration  📳 📳 📳

To vibrate the device in a pattern, we can pass an array of numbers.

Even indices numbers are responsible for the vibration and odd indices numbers will delay that much millisecond before the next vibration.

```javascript
// Vibrate for 500ms, Wait for 200ms, Vibrate for 800ms
window.navigator.vibrate([500, 200, 800]);
```

#### Cancelling Vibrations

To cancel an ongoing vibration pattern, we need to pass a `0` or an empty array or an array containing all zeroes to the `vibrate` method.

```javascript
window.navigator.vibrate(0);
window.navigator.vibrate([])
```

### Fun Example ✨

Vibrate <strong>`SOS`</strong> in morse code.

```javascript
window.navigator.vibrate([
    100,30,100,30,100,30,
    200,30,200,30,200,30,
    100,30,100,30,100
]);
```

Sample Code: [Github Repo](https://github.com/bibekkakati/blogs-projects/tree/main/web/vibration-api)

[Live Test](https://bibekkakati.github.io/blogs-projects/web/vibration-api/index.html)

---

Enjoyed? Give it a thumbs-up 👍

Thank you for reading | Feel free to [connect](https://bibekkakati.me) 👋
