---
description: >-
  A function is lines of code that you call from other places in your code to
  execute certain things. They're used far and wide, mostly when there's code
  you want to execute many times.
---

# Understanding Functions

A function is lines of code that you call from other places in your code to execute certain things. They're used far and wide, mostly when there's code you want to execute many times.

A function takes the following shape, basically:&#x20;

```javascript
function myFunc(arguments) {
  // function code
}
```

A function may return something, or not. Here's an example of a function that returns a value:

```javascript
function add(a, b) {
  return a + b;
}
```

And here's one that does not return a value, but still executes something:

```javascript
function log(type, message) {
  console.log(`[${type}] ${message}`);
}
```



###
