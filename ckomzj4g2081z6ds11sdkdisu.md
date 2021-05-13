## Capture Screen And Stream Like Zoom Using JavaScript

Hello everyone👋

In this article, we will see how applications like zoom use `Screen Capture API` provided by the browsers to capture your screen and stream it to the other end.

We will see a basic implementation of capturing the screen just to get an idea.

### Screen Capture API

The Screen Capture API let the user select a screen or portion of a screen (such as a window) to capture as a media stream. This stream can then be recorded or shared with others over the network.

### Implementation

First, we will create a simple HTML web page to show the captured screen's stream and buttons to start and stop capturing.

`Filename: index.html`

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>Screen Share</title>
  <script src="./script.js" defer></script>
</head>
<body align="center">
  <h2>Screen Capture</h2>
  <p>
    <button id="start">Start Sharing</button>
    <button id="stop">Stop Sharing</button>
  </p>
  <video id="video" width="800" height="680" autoplay></video>
</body>
</html>
```
I am assuming you have some basic knowledge of `HTML` and `CSS`.

Now we will create the JavaScript file where we will implement the main logic part.

`Filename: script.js`

```javascript
function main() {
  const video = document.getElementById("video");
  const start = document.getElementById("start");
  const stop = document.getElementById("stop");

  var displayMediaOptions = {
    video: {
	  cursor: "always",
	},
	audio: false,
  };

  start.onclick = function (e) {
	startSharing();
  };
  stop.onclick = function (e) {
	stopSharing();
  };

  async function startSharing() {
	try {
	  video.srcObject = await navigator.mediaDevices.getDisplayMedia(
		displayMediaOptions
	  );
	  } catch (error) {
		console.log(error);
	  }
	}

	function stopSharing() {
	  let tracks = video.srcObject.getTracks();
	  tracks.forEach((track) => track.stop());
	  video.srcObject = null;
	}
}

main();
```

- At first, we are assigning the reference of the `video` element and `button` elements.

- Listening on the `start` and `stop` button for an `onclick` event, which will invoke the `startSharing` and `stopSharing` method respectively.

- `displayMediaOptions` is a kind of config option which we are passing when capturing the stream. 

  - `audio: false` as we are not capturing the audio.
  - `video.cursor: always` means the cursor will always be visible on the stream.

> Check the official [docs](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Capture_API) for other options.

#### Start Sharing Function

To start capturing video from the screen, we are using the `getDisplayMedia` method on the instance of `navigator.mediaDevices`.

The Promise returned by the `getDisplayMedia` method resolves to a media stream that streams the captured screen which we are setting into the `video.srcObject`.

#### Stop Sharing Function

To stop capturing the screen, we are fetching the list of all the tracks using the `getTracks` method of `video.srcObject`. Then looping through the track list and calling its `stop` method. This will stop the stream.

After that, we are setting the `video.srcObject` to `null`.

### Example✨

Github Repo: [Screen Capture](https://github.com/bibekkakati/blogs-projects/tree/main/web/screen-capture-share)

Try it out: [Live](https://bibekkakati.github.io/blogs-projects/web/screen-capture-share)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620914800343/C7ubdIAY8.png)

---

Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)
