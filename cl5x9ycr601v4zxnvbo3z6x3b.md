## System Color Theme Check In JavaScript

Few days back I was wondering how to know if the system theme is dark or light in web using JavaScript and I found a way to detect that.

In this article, I will share the implementation that I used to check the system theme.

- We will use the method `matchMedia()` provided by the browser's window interface.

- `matchMedia` method expects a `mediaQueryString` as a parameter and it will return a `MediaQueryList` object.

- `MediaQueryList` object will have a property called `matches` of Boolean data type.

## Code

```javascript
if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
    // Dark Mode
}
```

`prefers-color-scheme` is a CSS media feature used to detect the system color theme.

We can also have a listener, if user changes the theme in-between.

```javascript
window
   .matchMedia("(prefers-color-scheme: dark)")
   .addEventListener("change", (event) => {
       const theme = event.matches ? "dark" : "light";
   });
```

Let me know in the comments if you are aware of any other way to detect the system theme in web.

---

Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)