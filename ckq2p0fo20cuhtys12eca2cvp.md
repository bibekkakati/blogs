## Error Handling in JavaScript  (Golang Style)

In this short article, we are going to see how we can handle error in JavaScript in Golang style.

I am assuming, you have some experience with JavaScript and you are aware of the issues with error handling like throwing an exception to the parent method from try-catch block or chaining multiple then-blocks and implementing logic inside it. These things can easily mess up with the code making it difficult to read.

Golang avoids these type of problems by handling errors/exceptions atomically.

#### Error handling in Golang

```golang
result, err := methodCall()
if err != nil {
  // handle error
}
// do something with the result
```

We can use a similar pattern in JavaScript with the help of a `try-catch` block like this.

```javascript
const getData = async () => {
  try {
    const result = await methodCall();
    return [result, null];
  } catch(error) {
    return [null, error];
  }
}
```

If any error occurs, we are returning the `error` in the second position of the array and the `result` as *null* in the first position.

If there is no error, we are returning the `result` in the first position and `error` as *null* in the second position.

Now we can call the `getData` method then handle the `result` and `error` like this.

```javascript
const [result, error] = await getData();
if (error !== null) {
  // handle the error
}
// do something with the result
```

This pattern of error handling makes it very easy to read and understand the code.

Let me know what do you think about this pattern.

---

Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)