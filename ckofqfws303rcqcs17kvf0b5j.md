## How To Use Web Worker

Hello everyone👋

In this article, we will see how can we use Web Worker API on our website to avoid blocking thread while doing CPU intensive task.

### Web Worker

A web worker is a JavaScript that runs in the background, independently of other scripts, without affecting the performance of the page.

#### What does that mean?


As we all know, JavaScript is a single-threaded language so when executing scripts the site becomes unresponsive until the scripts are finished. 

To avoid blocking the interaction of the site we can spawn a worker that will execute the scripts in the background. Thus, we can improve the performance of our website.

Web Workers uses a background thread separate from the main execution thread of a web application.

### Implementation

Let's explore the Web Worker API.

#### Check For Browser Support

```javascript
if (typeof(Worker) !== "undefined") {
  // It support
  ...
}
```

We will understand the implementation with a basic example. The parent script will pass a number to the worker script and it will calculate the square root of that number and return to the parent script.

Worker object and worker script have some event listeners with the help of which we can communicate and handle errors.

![web-workers.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1620481761784/zxweX_-T2J.jpeg)

### Parent Script

This javascript file will be running in the main thread.

#### Create Worker

```javascript
// Creates a new worker object
var worker = new Worker("./worker.js");
```

#### Receive Data

```javascript
// Listen for data from the worker script
worker.onmessage = function(e) {
  // Access the data from event object
  let data = e.data;
  ...
}
```

#### On Error

```javascript
// Listen for error
worker.onerror= function(err) {
  // Access the message from error object
  let error = err.message;
  ...
}
```

#### Send Data

```javascript
// Send data to the worker script
worker.postMessage(data);

```

#### Terminate Worker

```javascript
// Immediately terminates the worker
worker.terminate();
```

### Worker Script

Now we will create the javascript file `worker.js`.

```javascript
// Listen for data from the parent script
self.onmessage = function (e) {
  // Access the data from event object
  const value = Math.sqrt(e.data);

  // Sending data to the parent script
  self.postMessage(value);
};

// It fires when message can't be deserialized
self.onmessageerror = function (e) {
  ...
};
```

### Web Worker Access

Web Workers do not have access to the following JavaScript objects.

- `window`
- `document`
- `parent`

> Web Workers are used for more CPU intensive or heavy task like encryption, compression, long-polling etc.

### Example✨

Check out the [GitHub repo](https://github.com/bibekkakati/blogs-projects/tree/main/web/web-worker-api) for sample code.

Try it out [here](https://bibekkakati.github.io/blogs-projects/web/web-worker-api/index.html).

---


Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)
