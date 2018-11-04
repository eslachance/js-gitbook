---
description: >-
  A function is lines of code that you call from other places in your code to
  execute certain things. They're used far and wide, mostly when there's code
  you want to execute many times.
---

# Understanding Functions

A function is lines of code that you call from other places in your code to execute certain things. They're used far and wide, mostly when there's code you want to execute many times.

A function takes the following shape, basically: 

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

### Using/Calling Functions

So the 3 examples above were _defining_ functions, meaning they created functions that can be used later on. Let's see how we can use them in code. 

```javascript
const answer = add(2, 2);

log("answer", answer); // [answer] 4
```

Is it that simple? Yes, it really is. Let's break down a few things before we continue. 

```javascript
function functionName(argument, otherargument) {
  //function code
  return "Some Value";
}
```

* `function` is the keyword that defines a function. There are other ways to define them, but this is the "classical" way. 
* `functionName` is the name of the function itself, how it will be called. so `function add()` will be called as `add()`
* `argument` and `otherargument` are, of course, called the "Arguments" for the function. An Argument's name must not be confused with the Parameters that are sent to the function. That is to say, in the `add()` function, `a` and `b` are the _arguments_ and `2` and `2` are the _parameters_ sent to it. 
* `return` is a special keyword that does two very distinct things: first, it returns a value that's after it. So, `return 2;` will return the integer `2` to whatever called that function. Second, it _stops the execution of the function_. This means that anything _after_ a return keyword will not execute. This is useful if you want to stop execution based on a condition. For example: 

```javascript
// Stop execution if either arguments are missing: 
function add(a, b) {
  if(!a || !b) return false;
  return a + b;
};
```

The above will return `false` if either the `a` or `b` parameter is missing. The `a+b` line will simply never even be executed, which can save a lot of processing power in larger code.

### Optional Arguments

In the previous examples, `a` and `b` were _required_ arguments, meaning that you could not call the add function without both arguments being present \(otherwise, they would be `null` and our calculation would fail\). You can, however, give a function _optional_ arguments with a default value assigned. 

Let's say we want `add()` to increment by 1 only, if the second value is not present, instead of stopping the function. This is done by assigning a default value to `b` when we create the function: 

```javascript
function add(a, b = 1) {
  // We're still stopping the function if a is missing)
  if(!a) return false; 
  return a + b;
}

console.log(add(5)); // 6
```

### ES6 functions

In ES6 \(Or ECMAScript 6\), functions can have a slightly different look, using the "arrow functions". They are still assigned to a variable usually, in the following syntax: 

```javascript
const functionName = (argument, otherArugment) => {
  // function code
  return "Some Value";
}
```

So is there any difference between the regular and ES6 functions? There's a few, and they're all very useful.

#### Return is implied

If you have an arrow function that does not have curly braces, the `return` is implied. This means that you can greatly simplify very simple functions. For instance, our `add` function: 

```javascript
function add(arg1, arg2) {
  return arg1 + arg2;
}
// Simplified to: 
const add = (arg1, arg2) => arg1 + arg2;
```

#### This keyword is not overwritten

Mostly useful in relation to class inheritance. `this` , in regular functions, refers to the function itself, meaning `this.thing = blah` will add that property to the function or method. However, the ES6 arrow function does not overwrite `this` so it refersr to the upper scope. This is all technobabble to some, but if you know how to work with classes and modules, you'll understand why this is useful. 

#### Single-argument functions are simpler

When a single argument is present in an arrow function, you don't need the parentheses around that argument. Which means that `const split = str => str.split(" ");` is a perfectly valid function that will return an array of string parts, split by spaces \(ok, not a useful function, but you get the picture\). 

### Lambda/Anonymous Functions

So now we've seen how to create functions that can be called later in the code. But JavaScript has a lot of places where it can actually use what are called Anonymous, or Lambda, functions. Those are functions that are immediately executed, so setting them to a variable wouldn't really make that much sense. 

I love working with array functions, so let's take use a simple array of objects to show this feature.

```javascript
const data = [
  { name: "Bob", age: 42 },
  { name: "John", age: 56 },
  { name: "Katy", age: 24 },
  { name: "Nathan", age: 5 },
];

// Good ol' standard functions
const filter = function(line) {
  return line.age < 25;
};
const young = data.filter(filter);

// Identical function, as a lambda
const young = data.filter(function(line) {
  return line.age < 25;
});

// As a named ES6 lambda: 
const filter = line => line.age < 25;
const young = data.filter(filter);

// As an ES6 Arrow lambda
const young = data.filter(line => line.age < 25);
```

In all cases, the functions return the Katy and Nathan lines, as an array of objects. But the point here is that you can greatly simplify your code by using ES6 lambda functions in a whole lot of methods in JavaScript. 

I want to take a moment to show a few examples just to drive home the point of simplicity, when using both named and lambda functions. 

This is an example of using a Promise and catching the error that might occur while using this promise: 

```javascript
doMyPromiseThing().then(returnValue => {
  runSomething(returnValue);
}).catch(error => {
  console.log(error);
});
```

In this case, we're running 2 different functions \(`doSomething` and `console.log`\) on either of the then\(\) or catch\(\) blocks. But this can be simplify the entire thing with: 

```javascript
doMyPromiseThing().then(runSomething).catch(console.log);
```

This will runSomething on the return value, or console log any error that might occur. Of course, you might want to have some sort of `errorHandler` function for aching errors, but the point is that they can be called directly, without specifying a variable, without any curly braces or further syntax. 

### Callbacks

A "Callback" is an asyncronous concept that is the precursor of promises. A lot of modules still use callbacks in Node. 

> To be more precise, a "callback" is pretty much another name for a function called by another function. In promises, the `then` and `catch` blocks will run a _callback function_ , which is our lambdas we just saw. However, in common lingo, a "callback" is more often used to describe a module that will run things asyncroneously and use a callback when it's done its thing. I'll continue using Lambdas to refer to anonymous functions, and Callbacks to refer to asyncroneous function callbacks.

For instance, take this very simple database module code:

```javascript
db.get("SELECT * from USERS WHERE name = 'bob';", function(row) {
  console.log(row.name, row.age, row.email);
});
// Note: row is NOT available here
```

Here, the callback is the second argument of db.get\(\), and is called by the get\(\) function once it's done doing the thing it needs to do. I feel the need to point out that callbacks are fairly archaic at this point in Node's development, and most modules are now moving to using promises. 

One reason for this is that a Callback _CANNOT_ be "awaited" in a single line, in the sense that in order to use the data returned by the callback function, you have to absolutely use that data within the callback function. I refer to this in the [Understanding Promises](promises.md#async-await) page, where you can "in-line" a promise and use its return value directly without the .then\(\) block. Regular callbacks cannot be simplified that way. 

However, one advantage that callbacks have is that they can return _multiple values at once_, as separate arguments, something that Promises cannot achieve as of yet.

#### Making your own callback

Even though callbacks aren't exactly best practice anymore, you might find yourself needing to use them in very particular circumstances. Basically "making your own callback" means that you create a function that takes a function as an argument \(the callback\), which you will _execute_ when you're ready to return a value. 

```javascript
const asyncAdd = (arg1, arg2, callback) => {
  // let's pretend this "takes some time"
  setTimeout( () => {
    callback("solution", arg1+arg2);
  }, 1000);
});
```

So we just created a new function called `asyncAdd` that takes in 3 arguments: `arg1, arg2, callback`, where the callback needs to be an actual function. So how do we call this? Simple: 

```javascript
asyncAdd(40, 2, (message, solution) => {
  console.log(message, solution);
});

// Or if you really want to stick to simplicity and short code: 
asyncAdd(40, 2, console.log);
```

> And now you know how to make and use functions. Yay!

