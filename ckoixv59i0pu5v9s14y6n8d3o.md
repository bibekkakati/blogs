## Take Screenshot Of HTML Element Using JavaScript

Hello everyone 👋

A few months back, I was working on a web-based project where a feature was required that is to take a screenshot of an HTML div in the browser and show it to the user. I was like, *sorry this is not possible*. Then I did some research and got to know about this library called [html2canvas](https://html2canvas.hertzen.com/).

So in this article, I will show how can we capture a screenshot of a web page or any element of it using `html2canvas`.

### Implementation

- Download the javascript file: [html2canvas](https://html2canvas.hertzen.com)

### Code

Include the `html2canvas.min.js` file in your HTML file.

```HTML
...
<script src="./html2canvas.min.js" defer></script>
...
```

Now we will use the `html2canvas` method to capture the screenshot of our web page or the HTML element.

```javascript
html2canvas(document.getElementById("main"), {
  allowTaint: true,
  useCORS: true,
})
.then(function (canvas) {
  // It will return a canvas element
  let image = canvas.toDataURL("image/png", 0.5);
})
.catch((e) => {
  // Handle errors
  console.log(e);
});
```
The `html2canvas` method takes two arguments
- first is the HTML element whose screenshot you want.
- second is a configuration object.

In the `configuration object`, we are using
- `allowTaint` to allow cross-origin images to taint the canvas.
- `useCORS` to attempt to load images from a server using CORS.

> You can find the available configuration options [here](https://html2canvas.hertzen.com/configuration).

Then we are converting the returned `canvas` into a base64 image URL using the `toDataUrl` method which expects two arguments
- `type` : image format.
- `encodingOptions` : number between 0 and 1 indicating the image quality.

And that's it, we captured the screenshot of our HTML element.

### Important

This library has some issues, some of them are mentioned in the [docs](https://github.com/niklasvh/html2canvas). I recommend going through it and understand it before using it in any production-based environment.

> If you are aware of other ways to achieve a similar kind of result, please feel free to share.

### Example

Check out the GitHub [Repo](https://github.com/bibekkakati/blogs-projects/tree/main/web/html-screenshot).

Try it out here: [Live](https://bibekkakati.github.io/blogs-projects/web/html-screenshot/).

---


Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)
