## Singleton Pattern in Javascript

In this article, you will learn how to implement a singleton pattern in Javascript.

### What is Singleton Pattern?

Singleton pattern is a design pattern that allows us to use a single instance of a class everywhere.

### Implementation

We are creating an empty class `MyClass` for demonstration purpose.

```
class MyClass {
  ...
}

const Singleton = (function () {
  var instance;

  function createInstance() {
	var classObj = new MyClass();
	return classObj;
  }

  return {
	getInstance: function () {
		if (!instance) {
			instance = createInstance();
		}
		return instance;
	},
  };
})();

module.exports = Singleton;
``` 

The `Singleton` object is implemented as an IIFE.

> An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.

The `createInstance` function is responsible for creating the instance of `MyClass`.

The `getInstance` method will be invoked via the `Singleton` object. If the instance of `MyClass` is not present it will be created and returned, if already present it will return directly without creating a new instance.

So this pattern allows us to access and manipulate the members of a class instance from any file or function.

### Example

Let's create a class in a separate file.

```
// Filename: Username.js

module.exports.Username = class Username {
	constructor() {
		this._username;
	}

	set username(value) {
		this._username = value;
	}

	get username() {
		return this._username;
	}
};

``` 

> We are using getter and setter to access and set the value of the `_username`.


Now we will create a file for the `Singleton` object.

```
// Filename: singleton.js

const { Username } = require("./Username");

const Singleton = (function () {
	var instance;

	function createInstance() {
		var classObj = new Username();
		return classObj;
	}

	return {
		getInstance: function () {
			if (!instance) {
				instance = createInstance();
			}
			return instance;
		},
	};
})();

module.exports = Singleton;
``` 

> Here, we are importing the `Username` class and creating its instance with the help of the `Singleton` object.

At last, we will create a `index.js` file to run the program.


```
// Filename: index.js

const Singleton = require("./Singleton");

function main() {
	var instanceOne = Singleton.getInstance();
	instanceOne.username = "Jack";

	var instanceTwo = Singleton.getInstance();
	console.log("Second Instance: ", instanceTwo.username);
    // Output - Second Instance:  Jack

	console.log("Are both instance equal? ", instanceOne === instanceTwo);
    // Output - Are both instance equal?  true
}

main();
``` 

As you can see, first we call the instance of the `Username` class from the `Singleton` object and assigning it to variable `instanceOne`.
Then we set the `username` from `instanceOne`.

Again, we call the instance of `Username` class from the `Singleton` object and this time we are assigning it to another variable `instanceTwo`. And in the output, we can see that the value of `username` is the same as we set it through `instanceOne`.

When we compared if both instances are equal, it returns true.

### Conclusion

Singleton object is not creating any new instance every time we call it, instead, it returns the previous instance of the class. Hence, this design pattern is very useful in many cases like using a common database connection etc.

Github Repo [Link](https://github.com/bibekkakati/blogs-projects/tree/main/javascript/singleton-pattern)

Thank you for reading. Give it a thumbs-up if it is helpful for you.

Feel free to [connect](https://bibekkakati.me) 👋
