## Image Classification - Machine Learning in Javascript

Hello readers, recently I came to know about an awesome machine learning library for Javascript. 

Any guess? No, it is not `tensorflow.js`.

It is [`ml5.js`](https://learn.ml5js.org/). So what is [`ml5.js`](https://learn.ml5js.org/)?

> Before proceeding, I would like to mention that I am not a machine learning expert. I just have some basic knowledge and try out these kinds of stuff in my free time with the help of external libraries.

In this article, I will brief about the library and show some examples.

### What is `ml5.js`?

[`ml5.js`](https://learn.ml5js.org/) is a machine learning library built on top of `tensorflow.js` which we can use in our web browser. It is being developed to make machine learning more accessible and life easier for people who are new to the Machine Learning arena.

It uses the browser's GPU to run all the calculations. Getting started with the library is very easy.

Just include the package link in your project and you are good to go.

```
<script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
```

# Example

Let's implement something to understand the library.

We will implement Image Classification using this library.

### What is Image Classification?

Image Classification is a computer vision technique in which we classify images according to the visual content in it. We train the Image Classifier with crafted data so that it can predict what type of object is in an Image. If we train the classifier with dog's images, it will be able to identify a dog in a photo very easily.

---

We will create a webpage where user can upload an image or paste an image link, and our classifier will classify what type of object is in the image.

You can find the files here: [Github Repo](https://github.com/bibekkakati/blogs-projects/tree/main/javascript/ml5js/image-classification)

### Demo

![imgclassifier.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620125382401/2jEHOhudK.png)

### Prerequisite

```
- HTML
- CSS
- Javascript
```

### Code Implementation

First, we will be implementing the `index.html` page, which is our main web page.
On this page, we will have two buttons:
- `Upload Image` to upload an image from your local drive
- `Paste Link` to use hosted image from external server

On uploading or pasting a link of an image, the image will get rendered on the screen. After that on clicking the button `What is in the image?`, the result will be shown below it.

> Some external links of the images will not work because of cors policy.


### HTML

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Classifier</title>
    <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
    <link rel="stylesheet" href="./style.css">
</head>

<body onload="main()">
    <div class="loader-view" id="loaderView">
        <h3>Initializing ...</h3>
    </div>
    <div class="main" id="mainView">
        <h1 class="heading">Image Classifier</h1>
        <div class="select-image">
            <input type="file" name="Image" id="selectImage" accept="jpg,jpeg,png" hidden>
            <button class="upload-button button" id="uploadButton">Upload Image</button>
            <button class="link-button button" id="linkButton">Paste Link</button>
        </div>
        <div class="image-view" id="imageViewContainer">
            <img src="" alt="" class="image" id="imageView" crossorigin="anonymous">

            <button class="button" id="classifyButton">What is in the image ?</button>
            <h2 class="result" id="result"></h2>
        </div>

    </div>

    <script src="./script.js"></script>
</body>

</html>
```

### CSS

Just some styling for our webpage.

```
body {
	background-color: #000;
	color: #f0f8ff;
}

.main,
.loader-view {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	text-align: center;
	height: 100%;
	width: 100%;
}

.main {
	display: none;
}

.button {
	border: none;
	font-size: 16px;
	font-weight: 600;
	padding: 10px 15px;
	border-radius: 8px;
}

.upload-button {
	color: #f0f8ff;
	background: #ff7b00;
}

.link-button {
	color: #1f1f1f;
	background: #fdf8f4;
}

.upload-button:hover {
	background: #f0f8ff;
	color: #ff7b00;
}

.link-button:hover {
	color: #ff7b00;
}

.image-view {
	margin-top: 50px;
	width: 50vw;
	height: 60vh;
	display: none;
	flex-direction: column;
}

.image {
	max-width: 100%;
	max-height: 100%;
	border: solid #f0f8ff 6px;
	border-radius: 4px;
	margin-bottom: 5px;
}

.result {
	text-transform: capitalize;
	letter-spacing: 0.5px;
}

```

### Javascript

Calling the `main` function from `index.html` when body loads.

```
function main() {
	const classifier = ml5.imageClassifier("MobileNet", modelLoaded);

	const uploadButton = document.getElementById("uploadButton");
	const linkButton = document.getElementById("linkButton");
	const classifyButton = document.getElementById("classifyButton");
	const selectImage = document.getElementById("selectImage");
	const imageViewContainer = document.getElementById("imageViewContainer");
	const imageView = document.getElementById("imageView");
	const result = document.getElementById("result");
	const loaderView = document.getElementById("loaderView");
	const mainView = document.getElementById("mainView");

	uploadButton.onclick = function (e) {
		selectImage.click();
	};

	classifyButton.onclick = function (e) {
		classify(imageView);
	};

	linkButton.onclick = function (e) {
		const link = prompt("Paste Image Link Here");
		if (link != null && link != undefined) {
			imageView.src = link;
			imageViewContainer.style.display = "flex";
			result.innerText = "";
		}
	};

	selectImage.onchange = function () {
		if (this.files && this.files[0]) {
			var reader = new FileReader();
			reader.onload = function (e) {
				imageView.src = e.target.result;
				imageViewContainer.style.display = "flex";
				result.innerText = "";
			};
			reader.readAsDataURL(this.files[0]);
		}
	};

	function modelLoaded() {
		loaderView.style.display = "none";
		mainView.style.display = "flex";
	}

	function classify(img) {
		classifier.predict(img, function (err, results) {
			if (err) {
				return alert(err);
			} else {
				result.innerText = results[0].label;
			}
		});
	}
}
```

### Javascript Explanation

```
const classifier = ml5.imageClassifier("MobileNet", modelLoaded);
```
`ml5.imageClassifier` method is called to initialize the machine learning model.
Passing two arguments to the method first is the `model` which is `MobileNet` and a callback `modelLoaded` which will get invoked once the initialization is completed.

> MobileNet is a term that describes a type of machine learning model architecture that has been optimized to run on platforms with limited computational power, such as applications on mobile or embedded devices. MobileNets have several use cases including image classification, object detection, and image segmentation. This particular MobileNet model was trained for Image Classification.

We have some other choices too for the `model` like:
- `Darknet`
- `DoodleNet`

> You can use your own image classification model trained in Teachable Machine.

Then we are getting some references to buttons and views of our HTML file to listen for events and manipulate content and CSS styling.

```
uploadButton.onclick = function (e) {
		selectImage.click();
	};
```
On clicking the `Upload Image` button, it will click the image selector input element `selectImage`.

```
	selectImage.onchange = function () {
		if (this.files && this.files[0]) {
			var reader = new FileReader();
			reader.onload = function (e) {
				imageView.src = e.target.result;
				imageViewContainer.style.display = "flex";
				result.innerText = "";
			};
			reader.readAsDataURL(this.files[0]);
		}
	};
```
When the user selects the image, `selectImage.onchange` listener will get invoked and it will set the image in `imageView` src.

```
linkButton.onclick = function (e) {
		const link = prompt("Paste Image Link Here");
		if (link != null && link != undefined) {
			imageView.src = link;
			imageViewContainer.style.display = "flex";
			result.innerText = "";
		}
	};
```
On clicking the `Paste Link` button, `linkButton.onclick` listener will get invoked and it will ask the user for the <strong>image link</strong> and if a link is provided, it will set the link in the `imageView` src.

```
classifyButton.onclick = function (e) {
		classify(imageView);
	};
```
On clicking the `What is in the image?` button, `classifyButton.onclick` listener will get invoked and it will call the `classify` method, which is responsible for image classification. Will pass the image element reference i.e, `imageView` to the `classify` method.

```
function modelLoaded() {
		loaderView.style.display = "none";
		mainView.style.display = "flex";
	}
```
This method will get invoked when our model is initialized and it is manipulating some CSS style to hide the loader.

```
function classify(img) {
		classifier.predict(img, function (err, results) {
			if (err) {
				return alert(err);
			} else {
				result.innerText = results[0].label;
			}
		});
	}
```
This method is the important method that is calling the `predict` method of `classifier` object. The `predict` method expects two arguments:
- `input` which is a reference to the image element
- `callback` function to handle results and error

On error, we are throwing it in an alert box.

Accessing the result from the `results` array, which contains multiple objects with `label` and `confidence` level. 

---

<strong>Enjoyed?</strong> Give it a thumbs-up.

Thank you for reading | Feel free to [connect](https://bibekkakati.me) 👋

<a href="https://www.buymeacoffee.com/bibekkakati" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>