# Callbacks

A "Callback" is an asynchronous concept that is the precursor of promises. A lot of modules still use callbacks in Node.&#x20;

> To be more precise, a "callback" is pretty much another name for a function called by another function. In promises, the `then` and `catch` blocks will run a _callback function_ , which is our lambdas we just saw. However, in common lingo, a "callback" is more often used to describe a module that will run things asynchronously and use a callback when it's done its thing. I'll continue using Lambdas to refer to anonymous functions, and Callbacks to refer to asynchronous function callbacks.

For instance, take this very simple database module code:

```javascript
db.get("SELECT * from USERS WHERE name = 'bob';", function(row) {
  console.log(row.name, row.age, row.email);
});
// Note: row is NOT available here
```

Here, the callback is the second argument of db.get(), and is called by the get() function once it's done doing the thing it needs to do. I feel the need to point out that callbacks are fairly archaic at this point in Node's development, and most modules are now moving to using promises.&#x20;

One reason for this is that a Callback _CANNOT_ be "awaited" in a single line, in the sense that in order to use the data returned by the callback function, you have to absolutely use that data within the callback function. I refer to this in the [Understanding Promises](../promises.md#async-await) page, where you can "in-line" a promise and use its return value directly without the .then() block. Regular callbacks cannot be simplified that way.&#x20;

However, one advantage that callbacks have is that they can return _multiple values at once_, as separate arguments, something that Promises cannot achieve as of yet.

#### Making your own callback

Even though callbacks aren't exactly best practice anymore, you might find yourself needing to use them in very particular circumstances. Basically "making your own callback" means that you create a function that takes a function as an argument (the callback), which you will _execute_ when you're ready to return a value.&#x20;

```javascript
const asyncAdd = (arg1, arg2, callback) => {
  // let's pretend this "takes some time"
  setTimeout( () => {
    callback("solution", arg1+arg2);
  }, 1000);
});
```

So we just created a new function called `asyncAdd` that takes in 3 arguments: `arg1, arg2, callback`, where the callback needs to be an actual function. So how do we call this? Simple:&#x20;

```javascript
asyncAdd(40, 2, (message, solution) => {
  console.log(message, solution);
});

// Or if you really want to stick to simplicity and short code: 
asyncAdd(40, 2, console.log);
```
