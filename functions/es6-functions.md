# ES6 functions

In ES6 (Or ECMAScript 6), functions can have a slightly different look, using the "arrow functions". They are still assigned to a variable usually, in the following syntax:&#x20;

```javascript
const functionName = (argument, otherArugment) => {
  // function code
  return "Some Value";
}
```

So is there any difference between the regular and ES6 functions? There's a few, and they're all very useful.

#### Return is implied

If you have an arrow function that does not have curly braces, the `return` is implied. This means that you can greatly simplify very simple functions. For instance, our `add` function:&#x20;

```javascript
function add(arg1, arg2) {
  return arg1 + arg2;
}
// Simplified to: 
const add = (arg1, arg2) => arg1 + arg2;
```

#### This keyword is not overwritten

Mostly useful in relation to class inheritance. `this` , in regular functions, refers to the function itself, meaning `this.thing = blah` will add that property to the function or method. However, the ES6 arrow function does not overwrite `this` so it refers to the upper scope. This is all technobabble to some, but if you know how to work with classes and modules, you'll understand why this is useful.&#x20;

#### Single-argument functions are simpler

When a single argument is present in an arrow function, you don't need the parentheses around that argument. Which means that `const split = str => str.split(" ");` is a perfectly valid function that will return an array of string parts, split by spaces (ok, not a useful function, but you get the picture).&#x20;
