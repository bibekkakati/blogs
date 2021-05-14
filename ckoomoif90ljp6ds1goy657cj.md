## True Is Not Always True In JavaScript

Hello everyone👋

In this article, I will try to explain the behaviour of the `boolean` data type of JavaScript.

We often use `if` statements in JavaScript to check if a value, that can be of any data type is `true` or `false`. But do you know that these values are not really `true` or `false`, rather they are considered as `truthy` or `falsy` values?

### Explanation

Let's understand this with an example.

```javascript
var val = "blog";
if (val) {
  console.log(true);
}
```
So in the above code snippet, we declared a variable `val` which is storing a string `"blog"`.

In general, `if` statements expect a boolean expression or a boolean condition but here we are passing the variable `val` directly without any boolean expression.

And this `if` statement evaluates the value of `val` to `true` and execute its block. But why?

### Why

In JavaScript, any non-zero number including the negative numbers and non-empty strings are termed as `truthy` values and the `truthy` values are translated to boolean `true` when evaluated in a Boolean context.


![truthyfalsy.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1621016536792/Fvp6R5Rca.png)

So in our example, as the value of the variable `val` is a string with data i.e, not empty, it is considered as a `truthy` value which evaluates to `true` in the `if` statement condition.

And the values other than the `truthy` values are termed as `falsy` values.

`falsy` values in JavaScript.

- `false`
- `null`
- `undefined`
- `0`
- `NAN`
- `''`
- `""`
- `0n`
- `-0`

### Conversion

Convert the `truthy` and `falsy` values to boolean `true` or `false`.

You can pass the `truthy` or `falsy` value to the `Boolean()` and it will return `true` or `false`.

```javascript
var val = "blog";
if (Boolean(val)) {
  console.log(true);
}
```

Or you can use the following syntax to convert it to a pure boolean value.

```javascript
var val = "blog";
if (!!val) {
  console.log(true);
}
```

We know this `truthy` or `falsy` concept is not so impacting but it is always better to handle pure boolean values.

---

Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)


 
