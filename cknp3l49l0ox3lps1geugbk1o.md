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


