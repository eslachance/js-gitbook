---
description: >-
  Classes are a blueprint to making "things" with common properties and methods.
  Gather around, class, let's get to work building them!
---

# Understanding Classes

A "Class", in any programming language, is essentially defined as a _blueprint_ on which you can build multiple _instances_ \("copies of"\) that all share the same basic traits. These traits include _properties_ and _methods_. 

### Why use Classes?

Classes are a great way to prevent code duplication, and to greatly simplify how you deal with multiple copies of a single "type" of thing. So let's say you have a bunch of "User" objects in your code - you probably have a bunch of methods to deal with those users: creating them, updating them, deleting them, etc. With a class, you can do things like `SomeUser.delete()` or `SomeUser.login(username, password)` and other useful things.

It makes your code cleaner, more efficient, and easier to read!

### Creating a Class

Taking a page from MDN, this is a very basic, simple class: 

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

Let's break this down into its parts: 

* `class` is the keyword that triggers the creation of a class.
* `Rectangle` is the _name_ of the class.
* `constructor` is the [function ](functions.md)that runs when a new instance of the class is created.
* `this` refers to the class instance itself \(in this context\). So, setting `this.height` will set the "height" property of the instance. 
* `width` and `height` are class _properties_. They are a bit like an object property \(well, they are, since everything is an object in JavaScript\).

In order to create an instance, we use the `new` keyword, with the class. Here's an example with the above `Rectangle` class: 

```javascript
const myRect = new Rectangle(10, 5);

console.log(myRect.height); // 10
console.log(myRect.width); // 5
```

### Methods

The next thing to learn about a class is _methods_, which are functions attached to a class that will, usually, affect the class and its properties in some way. The syntax for methods is very slightly different from a normal function, in that you don't need the function keyword. Also, as a sidenote, there are no [arrow functions](functions.md#es6-functions) in method definitions for classes. 

Definiting a method is done after the constructor: 

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  
  setWidth(newWidth) {
    this.width = newWidth;
  }
  
  setHeight(newHeight) {
    this.height = newHeight;
  }
  
  getArea() {
    return this.height * this.width;
  }
}
```

As you can see, `this` will also refer to the class instance in its methods. Modifying `this` properties changes it for the instance, not for the base class itself, since the base class is a blueprint only.

Any instance of the class will now have those methods. For example: 

```javascript
const myRect = new Rectangle(10, 5);

console.log(myRect.width); // 5

myRect.setWidth(4);

console.log(myRect.width); // 4

console.log(myRect.getArea()); // 40
```

### Extending Classes

A class can _extend_ another class. An extended class will inherit the base classe's methods and properties by default, but each of those can be overwridden by the extended class. 

Let's create a new class called `Square` that extends `Rectangle` \(since a square is always a rectangle, but a rectangle isn't always a square\).

```javascript
class Square extends Rectangle {
  constructor(size) {
    // super() calls the constructor of the parent class
    super(size, size);
    // the this keyword can only be called AFTER super() is called
    this.size = size;
    this.width = this.size;
    this.height = this.size;
  }
  
  // A new method only availble for squares
  setSize(newSize) {
    this.size = newSize;
  }
  
  // override the base setWidth method
  setWidth(newWidth) {
    this.size = newWidth;
  }
  
  // override the base setHeight method
  setHeight(newHeight) {
    this.size = newHeight;
  }
}
```

So we obviously have more code here than the base class, just to keep things working as expected. Note however that we now have access to a total of 4 methods, even though the base class only has 2, and we only have 3 in the extended class. Because child classes inherit methods from their parent, `getArea()` is also available to the child class.

```javascript
const mySquare = new Square(5);

console.log(mySquare.getArea()); // 25
```

### Getters and Setters

While the `getArea()` method of course gets the area of the Square or Rectangle, there is an alternative way of doing things, using getters and setters. Essentially, a _Getter_ is a method that retrieves something from the class, while a _Setter_ is a method that changes a class property. Those methods can have calculations and a lot of steps beyond just returning a property. 

So let's change our `getArea` method into a getter instead: 

```javascript
get area() {
  return this.height * this.width;
}
```

Doing this means that you can access `area` just like if it was a property, instead of calling the method, which can simplify code greatly for whoever is using that code: 

```javascript
const mySquare = new Square(5);

console.log(mySquare.area); // 25
```

We can do something similar with a setter. However, it's important to note that you can't create a setter for a property of the same name. Basically, this is wrong: 

```javascript
// DO NOT USE THIS
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  set width(newWidth) {
    this.width = newWidth;
  }
  set height(newHeight) {
    this.height = newHeight;
  }
  get area() {
    return this.height * this.width;
  }
}
```

This results in an infinite loop, because doing `this.width = 10;`  will call the setter, which calls the setter...

To resolve this, you have 2 different paths you can take: using Symbols, or "internal properties". 

```javascript
// Using Symbols
const width = Symbol();
const height = Symbol();

class Rectangle {
  constructor(height, width) {
    this[height] = height;
    this[width] = width;
  }
  set width(newWidth) {
    this[width] = newWidth;
  }
  set height(newHeight) {
    this[height] = newHeight;
  }
  get area() {
    return this[height] * this[width];
  }
}
```

```javascript
// Using internal properties
class Rectangle {
  constructor(height, width) {
    this._height = height;
    this._width = width;
  }
  set width(newWidth) {
    this._width = newWidth;
  }
  set height(newHeight) {
    this._height = newHeight;
  }
  get area() {
    return this._height * this._width;
  }
}
```

So you might be asking "But Evie, which one do I use?" to which my answer would be: Symbols are probably the "easiest" way here. The reason I'm saying this is because those internal properties with an underscore... are still accessible to the end user \(to whatever code calls the class\), whereas Symbols aren't. I mean, technically they are if you work hard enough, but definitely not easily. 

### Calling the super!

When extending a class, you've seen that we can call the `super()` method in order to initialize the parent class with properties from the child constructor. Basically, in the constructor, `super()` refers to the parent's constructor. But there's another use for this `super` keyword. In a child class' methods, `super` refers to the parent class along with all its methods and properties. 

It's important to understand that calling methods and properties from `super` will _essentially_ call them for the child itself, _except_ when you overwrite a parent's methods. 

Let's get away from geometry for a second here, and extend something else. Taking a page from my very own Enmap module, let's extend JavaScript's `Map` structure with our own `set()` method that will only log values to console. Not super useful, but sufficient to show the point I'm trying to make: 

```javascript
class SuperMap extends Map {
  constructor(iterable = null) {
    super(iterable);
  }
  
  set(key, value) {
    console.log(`New value ${value} for key ${key}`);
    super.set(key, value);
  }
}
```

Using `super.set(key, value);` here prevents a feedback loop similar to what we saw in _setters_. If we were to use `this.set(key, value);` we'd be calling the method back on itself. However, calling `super.set(key, value);` means we're saying "HEY, PARENT! DO THIS!". This will still set the value in the Map as expected, because calling the parent's method affects the instance. 

I'm not sure I'm really making my point here, so let me say it in another way: `super.set()` calls the original method, not the child's override method, on the current intance of the child. Ok I guess that's still a little technobabble-y, I hope I did get the point across though. 

