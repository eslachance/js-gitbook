# Chaining Functions

Function chaining means that you can simply call functions one after the other, using dots between each function. This is something that's part of core JavaScript, whenever you have a value that can take functions, and that function returns a new value, you can chain them! Let's take a fairly complex example. Don't worry about what it does, just look at the syntax.

```javascript
const phrase = "I am a sentence";
const flip = phrase.split(" ").reverse().join(" ");
console.log(flip);
// outputs "sentence a am I"
```

In the example, we're starting with a simple string. Then we're applying the String.split() function to it, which returns an array. We then use Array.reverse() to flip the array itself. Since the return value of split() is the array, Array.reverse() works on that return value. Finally, we apply Array.join() which converts the array to a string.

So just to re-iterate clearly: The reason why chaining functions work is because the function returns a value. Functions that do not return values cannot be chained. For instance, `console.log("Test").anythingElse()` can't work because `console.log()` doesn't return anything.
