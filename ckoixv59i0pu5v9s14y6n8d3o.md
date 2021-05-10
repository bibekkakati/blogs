## Take Screenshot Of HTML Element Using JavaScript

Hello everyone 👋

A few months back, I was working on a web-based project where a feature was required that is to take a screenshot of an HTML div in the browser and show it to the user. I was like, *sorry this is not possible*. Then I did some research and found this library called [html2canvas](https://html2canvas.hertzen.com/). There are some issues which I came to know later, but it has the solution.

So in this article, I will show you how can we capture a screenshot of a web page or any element of it using `html2canvas`.

### Implementation

- Download the minified js file: [html2canvas](https://html2canvas.hertzen.com/dist/html2canvas.min.js)

### Code

Include the `html2canvas.min.js` file in your HTML file.

```HTML
...
<script src="./html2canvas.min.js" defer></script>
...
```

Now we will use the `html2canvas` method to capture the screenshot of our web page or the HTML element.

```javascript
// Pass the HTML element whose screenshot you want
html2canvas(document.getElementById("main"), {
  letterRendering: 1,
  allowTaint: true,
  useCORS: true,
})
.then(function (canvas) {
  // It will return a canvas element
  // Converting the canvas to base64 image url
  let image = canvas.toDataURL("image/png", 0.5);
})
.catch((e) => {
  // Handle errors
  console.log(e);
});
```
`toDataUrl` method expects two arguments
- `type` : image format.
- `encodingOptions` : number between 0 and 1 indicating the image quality.

---

Enjoyed? Give it a thumbs-up 👍

Thank you for reading | Feel free to [connect](https://bibekkakati.me) 👋