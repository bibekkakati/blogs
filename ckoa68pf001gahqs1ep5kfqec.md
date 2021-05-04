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


![html-file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620152207552/ZMCHVRwF0.png)

### CSS

Just some styling for our webpage.


![css-file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620152470414/sUlm_-3ON.png)


### Javascript

Calling the `main` function from `index.html` when body loads.


![script-file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620152337360/f4Jk2whQl.png)

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


### Result

![imgclassifier.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620125382401/2jEHOhudK.png)

You can find the files here: [Github Repo](https://github.com/bibekkakati/blogs-projects/tree/main/javascript/ml5js/image-classification)

---

<strong>Enjoyed?</strong> Give it a thumbs-up.

Thank you for reading | Feel free to [connect](https://bibekkakati.me) 👋

<a href="https://www.buymeacoffee.com/bibekkakati" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>