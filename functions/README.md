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

## Using and Calling Functions

So the 3 previous examples were _defining_ functions, meaning they created functions that can be used later on. Let's see how we can use them in code.

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

In the previous examples, `a` and `b` were _required_ arguments, meaning that you could not call the add function without both arguments being present (otherwise, they would be `null` and our calculation would fail). You can, however, give a function _optional_ arguments with a default value assigned.

Let's say we want `add()` to increment by 1 only, if the second value is not present, instead of stopping the function. This is done by assigning a default value to `b` when we create the function:

```javascript
function add(a, b = 1) {
  // We're still stopping the function if a is missing)
  if(!a) return false; 
  return a + b;
}

console.log(add(5)); // 6
```
