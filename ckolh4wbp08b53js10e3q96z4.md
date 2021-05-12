## Detect Internet Connection Status In Browser

Hello everyone 👋

In this article, we are going to learn how can we detect the internet connection state on our website.

This can be very useful to improve user experience by showing snack messages or pop-ups when the browser is not able to connect to the internet.

### Implementation

We can get the current state of the connection by using `window.navigator.onLine`, which will return a `boolean` value.

- `true` if connected.
- `false` if not connected.

```javascript
const online = window.navigator.onLine;
if (online) {
  // Is connected to internet
} else {
  // Not connected to internet
}
```

> If the browser doesn't support `window.navigator.onLine` the above example will always come out as `false` or `undefined`.

#### Connection State Changes Listener

We can also detect the connection state by listening for network state change events i.e, `online` and `offline`.

```javascript
window.addEventListener('offline', function(e) {
    // Network disconnected
  }
);

window.addEventListener('online', function(e) {
    // Network connected
  }
);
```

It's very easy to implement but there are some side cases where it might give a false-positive result.

- The computer is connected to a mobile hotspot, but mobile internet is not working then also you can get an `online` status.

- The computer is running a virtualization software that has virtual ethernet adapters that are always "connected".

---

Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect with me on [Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati) 👋