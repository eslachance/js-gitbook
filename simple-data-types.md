# Simple Data Types

In our previous example we used _strings_ as values for our variables. But, of course, JavaScript has a lot more to offer than just these series of characters, though! Let's take a look at the various _simple_ data types available in the langauge. 

### Strings

Strings are essentially a "static" series of characters of any kind, surrounded by either single quotes, or double quotes. They don't _really_ have a size limit, but by default they got to be on a single line. 

Strings look like this: 

```javascript
let myString = "I'm a string.";
const otherString = 'This is also a string';

// If you're using the double or single quotes they have to be "escaped":
const escapedSingle = 'I\'m cool and it\'s fine!';
const escapedDouble = "This is an \"escape\" from real life";

// You can put strings together, called "concatenating" using a + sign:
const concatString = escapedSingle + " I'm in the middle " + escapedDouble;

// You can also append a string with the special += method:
myString += " and I've added to myString now!";
```

> There are more complex strings called Template Literals, used amongst other things for better string concatenation, but they deserve their own page so [head on over there to learn more about them](template-literals.md)!

### Integers and Numbers

Numbers are somewhat limited in JavaScript, in the sense that JS only supports "32-bit integers". Not often will that really be an issue as this means the maximum integer size is `9007199254740991`. JavaScript also supports Float values, obviously. 

```javascript
const myInt = 42; // note the lack of any quotes!
const myFloat = 346.32462346;

// You can do some math with JS, of course. The language follows regular math order
// of operation, parentheses go first, then * and / , etc. 
const myResult = 10 * (33 - 5) / 2 + 8; // result: 148
```

> You shouldn't do "real" math with JavaScript. Some details of the language could mean bad results. Some of these issues take the form of rounding errors or just plain old weirdness. For instance, `0.1 + 0.2` will actually not equal `0.3` but rather `0.30000000000000004`. Why? Because, JavaScript. Though this particular example really doesn't work in _most_ programming languages.

### Booleans

A _boolean_ is essentially a value that is true or false. Defining a boolean is essentially super easy: 

```javascript
const imTrue = true;
const imFalse = false;
```

Now, that's not **extremely** useful to be honest, but booleans are much, much more than that. There are many operations that will _return_ a boolean value when you execute them. Here are a few examples: 

```javascript
const isBigger = 5 > 2; // true
const isEqual = "blue" === "red"; // false
```

Some things are not quite booleans but will act the same. I will reserve this explanation for conditions however, which are explored in another part of this guide. That's also where we'll talk about those operators I just used!

### Null and Undefined

Some values can be either null or undefined, so these two types are considered data types, but are generally used under very specific circumstances.

```javascript
let test; // test is "undefined" but won't crash the bot
console.log(test); // undefined

console.log(x); // crashes with "ReferenceError: x is not defined;

const what = null; // valid
console.log(what); // null
```

