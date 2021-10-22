# Lambda / Anonymous Functions

So now we've seen how to create functions that can be called later in the code. But JavaScript has a lot of places where it can actually use what are called Anonymous, or Lambda, functions. Those are functions that are immediately executed, so setting them to a variable wouldn't really make that much sense.&#x20;

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

In all cases, the functions return the Katy and Nathan lines, as an array of objects. But the point here is that you can greatly simplify your code by using ES6 lambda functions in a whole lot of methods in JavaScript.&#x20;

I want to take a moment to show a few examples just to drive home the point of simplicity, when using both named and lambda functions.&#x20;

This is an example of using a Promise and catching the error that might occur while using this promise:&#x20;

```javascript
doMyPromiseThing().then(returnValue => {
  runSomething(returnValue);
}).catch(error => {
  console.log(error);
});
```

In this case, we're running 2 different functions (`doSomething` and `console.log`) on either of the then() or catch() blocks. But this can be simplify the entire thing with:&#x20;

```javascript
doMyPromiseThing().then(runSomething).catch(console.log);
```

This will execute `runSomething` on the return value, or console log any error that might occur. Of course, you might want to have some sort of `errorHandler` function for aching errors, but the point is that they can be called directly, without specifying a variable, without any curly braces or further syntax.&#x20;
