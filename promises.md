---
description: >-
  I promise you'll have fun learning these - let's take a look at asyncroneous
  promises, how to resolve them, use async, and even how to make your own.
---

# Understanding Promises

In your endeavours learning and using JavaScript you will encounter a thing called a _Promise_. Like the name kinda sorta implies, a promise is something that happens in the future \(and, in fact, they're sometimes called _Futures_ in other languages!\).

The way I like to looks at promises is basically that they're an "IOU". You give a promise something to do and it _owes_ you a response later on in your code. When it's ready, it pays you back with an answer!

## Basic Promises

Let's take a look at what this means in terms of code. Let's say we have a promise called `mathAdd` which takes in two numbers and adds them together. In our imaginary world, that takes a few moments and isn't instantaneous. Humor me for a moment, and look at one way we could use this promise function in code:

```javascript
mathAdd(2, 2).then( answer => console.log(answer) );
```

So, the first thing you'll notice when using promises, is that to get the value, you need to use `.then()`. Something like `const response = math.add(2, 2);` would return the _promise itself_, and not the result of the operation.

When I said "it takes a moment", what I mean to say is that the `answer` itself is not available directly after this line has run. This means that the following code _**will not work**_:

```javascript
let answer;
mathAdd(2, 2).then(res => answer = res);
console.log(answer); // logs `null`;
```

This is because the promise can take a few milliseconds or a few minutes, it makes no difference, the line _after_ it \(the console log\) will run before the promise has resolved. So for now, you have to remember that your code needs to be inside of the .then\(\) callback. My above examples were a bit of a shortcut, so let's do this with a more complete example and a full function.

```javascript
mathAdd(2, 2).then( answer => {
  console.log("The answer is: ");
  console.log(answer);
});
```

And before you ask "but can't I just do `mathAdd(2, 2).then(answer => { return answer; });` , well... no. You can't return from a callback whether it's a promise or not. There _are_ better ways of dealing with promises, but before we do, let's take a look a handling errors.

## Catching Errors

Normally in JavaScript, you catch errors using a try/catch block, surrounding your code. With Promises, the default way of doing this is using a second method after the then\(\), which is catch\(\). They need to be in order, so a Promise that can throw an error would be handled this way:

```javascript
// Basically: 
myPromiseFunction().then(responseFunction).catch(errorFunction);

// Example: 
myPromiseFunction(args).then(response => {
  console.log(response);
}).catch(error => {
  console.error(error);
});
```

Rember that because in JavaScript you can replace the _callback_ portion of the above code with an actual function, you could do something like this:

```javascript
myPromiseFunction().then(console.log).catch(console.error);
```

## Async/Await

Async/Await is a relatively new feature in Node, which was added in version 7.6. It offers the great advantage of being able to simplify your code by removing the need for a .then\(\) method, and simply "returning the value" instead of a promise. The second advantage is that using async/await means you can write code sequentially as if you weren't even using promises, so you don't need to write everything in the then\(\) method itself!

The caveat is that using the await keyword requires that the function using it be async. This also means the async function returns a promise itself, so anything calling that function also needs to resolve a promise instead of simply grabbing the return. With all this said, let's look at a very simple example of an async function using await:

```javascript
// Regular Promises: 
function myFunc() {
  myPromiseFunction().then(response => {
    console.log(response);
  }
}

// async version
async function myFunc() {
  const response = await myPromiseFunction();
  console.log(response);
}
```

Where async/await functions shine is when you need to chain multiple promises together to ultimately get your data. Let's take this example:

```javascript
getData().then(a => { 
  getMoreData(a).then(b => {
    getMoreEvenMoreData(b).then(c => {
      getUltimateData(c).then(d => {
        console.log(d);
      });
    });
  });
});
```

This is something that people often call "callback hell", or in this case, "promise hell". Async/await makes this much more simple, assuming you're already in an async function:

```javascript
async function myFunc() {
  const a = await getData();
  const b = await getMoreData(a);
  const c = await getEvenMoreData(b);
  const d = await getUltimateData(c);
  console.log(d);
  // and you can also RETURN this!
  return d;
}

myFunc().then(console.log); // prints the value of d
```

Async/await errors are handled differently, actually when using this concept you simply go back to using try/catch. Here's the same code as above, with error handling added:

```javascript
async function myFunc() {
  try {
    const a = await getData();
    const b = await getMoreData(a);
    const c = await getEvenMoreData(b);
    const d = await getUltimateData(c);
    console.log(d);
    // and you can also RETURN this!
    return d;
  } catch(err) {
    console.error("An error occured: " + e);
  }
}
```

Async works in any type of functions, even callbacks. Here are a few examples of using async.

```javascript
// Events
emitter.on("someEvent", async (arg1, arg2) => {
  const response = await myPromiseFunction();
  console.log(response);
});

// ES6 functions
const myFunc = async (arg1, arg2) => {
  const response = await myPromiseFunction();
  console.log(response);
}

// Inside a callback
someFunction("myArg", async (response) => {
  await doSomething();
});
```

## Build Your Own Promise

So now you should \(if I'm as good a teacher as I think\) know how to _use_ promises, but what about _making_ them? It honestly took some time even for me to wrap my head around creating promises but I'll try to make it as simple as possible. Let's make a _really_ simple function that returns a promise:

```javascript
const underAged = (myAge) => {
  return new Promise( (resolve, reject) => {
    if(myAge < 18) {
      reject("I can't serve you alcohol");
    } else {
      resolve("Here's your drink!");
    }
  });
}

// And then we can use it
underAged(21).then(console.log).catch(console.error);
// logs "Here's your drink!"

underAged(17).then(console.log).catch(console.error);
// logs error "I can't serve you alcohol!"
```

If it wasn't already obvious, the `resolve()` method triggers the promise's `.then()` answer, but the `reject()` method triggers the promise's `.catch()`.

It's important to note that to the contrary of _callback_ functions, a promise can **only return a single value**, so you can't do something like `resolve("thing1", "thing2")`, that would simply return the first argument. However, you can most definitely return an array or object from a promise!

There is also a secondary way of creating a promise. As I mentioned earlier, creating an async function will automatically create a promise. However, because you're not able to define the `resolve()` and `reject()` methods, you can simply trigger the promise's `then()` through a `return`, and you can trigger a `catch()` by throwing an error. Here's the same function as above, using this concept:

```javascript
const underAged = async (myAge) => {
  if(myAge >= 18) return "Here's your drink!";
  else throw new Error("I can't serve you alcohol!");
}
```

Hopefully, now you've learned enough about promises to do some great things with them!

