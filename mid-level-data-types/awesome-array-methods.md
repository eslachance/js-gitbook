---
description: >-
  Arrays are my very favourite data structure in JavaScript. Let's see why by
  exploring precisely what makes them great.
---

# Awesome Array Methods

I wish every data structure in JavaScript was as cool as Arrays. No, really, I'm not being hyperbolic or sarcastic, and I'm going to prove it.&#x20;

{% hint style="warning" %}
Most array methods use _functions_ so you should probably head on over to [Understanding Functions](../functions/) before you read this page. I promise it'll be much easier once you've done that!
{% endhint %}

## Array.map()

Array.map() is used to iterate over an array and return a new array which contain values that each loop iteration returns. map() takes a single argument which must be a [function](../functions/). This function will be called with 3 different arguments: `currentValue` , `currentIndex`, `inputArray`. Mostly in the wild you'll only see the first argument being used (the current value in the array for this loop iteration), but you might find the other 2 values... useful.&#x20;

Let's put all this into a concrete example that makes sense. Let's say I have an array of words that I want to put in all caps. To modify my array, I have to loop through it, which of course can be done with some archaic method using temporary variables and for...i loops (eww):&#x20;

```javascript
const startArray = [ 'bleh', 'foo', 'MoOoO', 'supercalifrag' ];

const arrToUpper = input => {
  const temp = [];
  for ( let i = 0; i < input.length; i++ ) {
    temp.push(input[i].toUpperCase());
  }
  return temp;
}

const upperArray = arrToUpper(startArray);
```

But by golly, that's a lot of code for something that can so easily be done not only without an intermediary function but also with ONE SINGLE LINE OF CODE:&#x20;

```javascript
const startArray = [ 'bleh', 'foo', 'MoOoO', 'supercalifrag' ];

const upperArray = startArray.map( word => word.toUpperCase() );
```

Now isn't that nicely short & sweet? Can you think of anything else that map() can be used for?

## Array.filter()

Array.filter() is used to _remove things you don't want_ from an array, by... well, by filtering them out. It will return a new array where some array elements have been removed. Which elements? They're determined by a function - filter() takes a function which needs to return a truthy or falsy value (see the [Conditions ](../conditions.md)page to know what that means) - truthy values keep the element in, falsy values throws the element in the garbage and you never see it again.&#x20;

As a concrete example, let's say I want to only keep values that are _odd_ in an array, and eliminate any _even_ number. We'll use a tiny bit of mathematics to do this, more specifically the _modulo_ function, which in JavaScript is used with `%`. Basically, if you `% 2` a number, it'll return 0 ("falsy") if it's even, 1 ("truthy") if it's odd. Simple, right? Let's do this!

```javascript
const someNumbers = [ 1, 2, 61, 332, 5643, 42, 0, 111 ];

// we could of course do it the lame way
const filterOdds = input => {
  const temp = [];
  for ( let i = 0; i < input.length; i++ ) {
    if (input[i] % 2) {
      temp.push(input[i]);
    }
  }
  return temp;
}

const onlyOdd = filterOdds(someNumbers);

// but bleh. no way, Jose!
const betterOnlyOdd = someNumbers.filter( n => n % 2);
```

Isn't that beautiful? Now how would you make a filter for _even_ numbers instead? Just invert the condition!

```javascript
const onlyEven = someNumbers.filter( n => !(n % 2) );
```

Let me leave you with a last super useful trick that's a common enough question to warrant its own little example. You can filter out `null` and `undefined` values easily from an array using one of JavaScript's built-in function, `Boolean()`. Boolean() will return an actual true/false value, and it can be used directly in a filter() function [as described in the functions page](../functions/#lambda-anonymous-functions). Here it is:&#x20;

```javascript
const noEmpties = myArray.filter(Boolean);
```

You can of course use any function that expects an input and returns a boolean value here, whatever that function is. I'll leave the rest to your imagination for now.

{% hint style="info" %}
The Boolean function returns false on empty strings `''` or the number `0` so be careful when you use it!
{% endhint %}


## Array.find()

This one is really simple. Array.find() is exactly the same as array.filter, except that when it finds a result (when the condition returns true), it will return the value from the current iteration, and stop the loop. So, it takes the same kind of function as Array.filter() but instead of returning an array of values, it returns the first value. If you want to only get one value, this is more efficient than using filter() then getting the first from it.

```javascript
const someNumbers = [ 1, 2, 61, 332, 5643, 42, 0, 111 ];
const firstEvenNumber = myArray.find(num => num % 2); // 2
```

## Array.some()

Another simple one! Array.some() takes in a function that will iterate on every element in the array. If **any** of the values in the array returns `true` on that function, then Array.some() *stops processing* and returns `true`. This makes it a pretty efficient method of checking if something is in the array, as it will not traverse the entire thing unless the value isn't located in the array.

```javascript
const vals = ["John", "Paul", "Ringo", "George", "Pete"];
const containsAnA = vals.some(name => name.includes("a"));
// true, and stops when it reaches "Paul".

const containsAnM = vals.some(name => name.includes("m"));
// false and goes through the whole array
```

## Array.every()

In the line of "just like the last one", Array.every() does the same thing as .some() except it will always traverse the entire array, and return true if, and only if, the function you provide it returns true on every single element of the array.

```javascript
const vals = ["John", "Paul", "Ringo", "George", "Pete"];
const missingA = vals.every(name => !name.includes("a"));
// false, one of them contains an A

const missingM = vals.every(name => !name.includes("m"));
// true, none of them contains a M
```

## Array.includes()

Array.includes() is a very simple method of checking whether a value is included inside an array. Very simply put, if you have an array of values, you can know if it includes a particular value or not. This returns a boolean, so it's very often used in conditions.

```javascript
const someNumbers = [ 1, 2, 61, 332, 5643, 42, 0, 111 ];

console.log(someNumbers.includes(1)); // true
console.log(someNumbers.includes(42)); // true

if(someNumbers.includes(5)) {
  console.log("5 Conditions make the world go round, blah!"); // won't print
}
```

Array.includes can also be very useful to verify if a string is equal to "one of many choices". As mentioned in [Combining Conditions](../conditions.md#conditions-can-be-combined), it replaces the pattern `if(thing === "blah" || thing === "foo")`, in the following manner:&#x20;

```javascript
const string = "hi";

if(["hey", "hello", "hi", "wazaaap"].includes(string)) {
  // will be true since the array includes "hi"
}
```

{% hint style="warning" %}
Array.includes() only works with *simple* values like strings and numbers. It won't work by comparing arrays and objects since JavaScript cannot compare them directly. You can, howevever, use Array.some() with a function to emulate this.
{% endhint %}

## Array.reduce()

Array.reduce() is essentially used to "add together" things from an array, used in concepts such as counters or concatenation of specific strings. It works by accepting a function with 2 useful parameters: `accumulator` and `currentvalue`. It also takes a second parameter, the default value, which is sent to the accumulator variable on the initial iteration of the loop. Also, enough fancy words, let's look at some code!

```javascript
const arr = [1, 2, 3, 4, 5];

const total = arr.reduce( (acc, current) => acc + current );
console.log(total); // 15
```

So, obviously this code is adding each number in the array to the accumulated value, right? You get an accumulated value of 1, then 3, then 6, 10 and finally 15. Simple as that.&#x20;

Sounds boring though, let's make it a bit more exciting. Arrays can contain objects, and we can also use that to our advantage. Let's say we have an array containing data about groups. Each group can contain multiple users, and those users are in an array in the object. Our goal now is to find the total number of users for all the groups. Let's do that:&#x20;

```javascript
const groups = [
 {
   name: 'Legends',
   users: [ "Ripp", "Ray", "Sara", "Martin", "Jefferson", "Kendra", "Carter"],
   leader: "Ripp"
 },
 {
   name: 'Fantasic',
   users: [ "Reed", "Susan", "Johnny", "Ben"],
   leader: "Reed"
 },
 {
   name: 'Avengers',
   users: [ "Steve", "Tony", "Thor", "Clint", "Natasha", "Peter"],
   leader: "Tony"
 }
];

const superheroes = groups.reduce( (acc, group) => acc + group.users.length, 0);
console.log(superheroes); // 17
```

The default value here is due to the array containing objects - the reduce function must have a 0 value so that additions will be integer additions, and not just objects or strings or something else.

{% hint style="info" %}
The reduce function adds two other arguments not used in my example: currentIndex and array. Those contain the current iteration loop index and the initial input array, if you ever need those things in your function!
{% endhint %}

## Array.sort()

\[ TBD cuz lazy right now ]
