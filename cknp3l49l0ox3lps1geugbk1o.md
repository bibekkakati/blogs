## Implementing Singleton Pattern In Dart - Flutter

## What is a singleton pattern?
Singleton pattern is a design pattern that allows us to use a single instance of a class everywhere. 

## Implementation

```dart
class ClassName {
    static ClassName _className;

    ClassName._createInstance();
    factory ClassName() {
        if (_className == null) {
            _className = ClassName._createInstance();
        }
       return _className;
    }
}
``` 
Factory constructors return an instance of the class, but it doesn't necessarily create a new instance.

---


Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)


