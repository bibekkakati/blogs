## Implementing Singleton Pattern In Dart - Flutter

## What is a singleton pattern?
Singleton pattern is a design pattern that allows us to use a single instance of a class everywhere. 

## Implementation

```
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

Thank you for reading. Give it a thumbs-up if it is helpful for you.

Feel free to  [connect](https://bibekkakati.me) 👋


<a href="https://www.buymeacoffee.com/bibekkakati" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

