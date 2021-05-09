## Generate QR Code In Javascript

Hello everyone 👋, this is going to be a very short article where I will show how can we generate a QR Code for any content in JavaScript.

Obviously, I am not going to implement everything from scratch and why should one do that when we have a plethora of useful libraries in JavaScript.

I came across this awesome lightweight library or you can say a simple script [qrcodejs](https://github.com/davidshimjs/qrcodejs). It is very easy to use and is reliable too.





### Implementation

- Download this zip file: [qrcodejs](https://github.com/davidshimjs/qrcodejs/zipball/master)

- Extract it.

- Now you can use the `qrcode.js` and `qrcode.min.js` file in your project.

### Code

Include the `qrcode.js` file in your HTML file.

```HTML
...
<script src="./qrcode.js" defer></script>
...
```

Give an `id` to the `div` where you want to show the generated QR Code. Here I have used `"qrcode"` as my `id`.

```HTML
...
<div id="qrcode"></div>
...
```

Now we will create an object from the `QRCode` function. Need to pass the `id` of the output `div` which is `"qrcode"` in this case.

```javascript
var QR_CODE = new QRCode("qrcode", {
  width: 220,
  height: 220,
  colorDark: "#000000",
  colorLight: "#ffffff",
  correctLevel: QRCode.CorrectLevel.H,
});
```

> `correctLevel`: `L` for low, `M` for medium, `H` for high.

Generate QRCode by calling the `makeCode` method of the QRCode object, which expects the `data` as its argument.

```javascript
QR_CODE.makeCode("https://blog.bibekkakati.me");
```
> It will automatically insert the generated QRCode in the `div` whose `id` has been provided while creating the QRCode object.

### Example✨

Check out the GitHub [Repo](https://github.com/bibekkakati/qr-gen).

Try it out here: [Live](https://bibekkakati.github.io/qr-gen/).

![Demo Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1620586396838/PuSFQynUo.jpeg)

*Screenshot taken from Google Lens while scanning.*

---

Enjoyed? Give it a thumbs-up 👍

Thank you for reading | Feel free to [connect](https://bibekkakati.me) 👋