# Mid Level Data Types

Slightly more advanced than the simple types, I consider these to be "mid-level" \(this isn't a standard terminology, though, just what I call them!\). 

### Arrays

An Array could be called a "list" in some other languages. It consists of a very simple series of things between square brackets \(`[]`\). You can put anything inside of arrays, and you can even mix and match different data types inside of it. 

```javascript
const myArray = []; // empty array
const myNumberArray = [1, 5, 2345, 33.12]; // array with just numbers

// Can you mix arrays and even have arrays in arrays? Sure you can!
const mixedArray = ["this is", "a mixed", 33, ["sub array", "yay"], "array"];

// You can define arrays in multiple lines, like this array of objects
// (see "Objects" below)
const objArray = [
  {"first": "post", "second": "thing"},
  {"first": "not", "second": "otherthing"}
];
```

Arrays are "accessed" through their numerical index, in other words, their position in the array. Using the above examples: 

```javascript
myNumberArray[0]; // 1
mixedArray[2]; // 33
objArray[1]; //  {"first": "not", "second", "otherthing"}

// You can change an array value through its index
myNumberArray[3] = 42;
// now equal to  [1, 5, 2345, 42]
```

Notice that the _first_ element is at index `0`, not one. This is what we call "zero-based", so it really does start at 0, not 1. 

Learn more about arrays in ~~Working with Arrays~~.

### Objects

An _object_ is a series of _key_ and _value_ pairs put together between `{}` , as shown in the array example. Contrarily to arrays, the "index" \(which we called the "key"\) has an actual text name. Objects cannot have multiple keys of the same name. 

Note that object key/value pairs are defined with a semicolon \(`:`\) not an equal sign. Each key/value pair must be separated by a comma \(`,`\). The **last** value should not have a comma after it. Those details are important!

```javascript
const myObject = {}; // empty object
const myFavs = {
  color: "blue",
  car: "mine",
  number: 42,
  hasChildren: true
}

// You can "get" a part of an object through it's property:
myFavs.car; // "mine"
myFavs["hasChildren"]; // true

// You can also "set" an object key whether it exists or not
myFavs.color = "black";
myFavs.song = "All about that bass";

/* Current object data: 
{
  color: "black",
  car: "mine",
  number: 42,
  hasChildren: true,
  song: "All about that bass"
}
*/
```

> Theoretically, almost everything except the simple value types are objects. Arrays, classes, functions, maps and sets... all objects. While that's something to keep in mind for later, for now I'll refer to "objects" specifically as "a series of key/value pairs surrounded by `{}`.



