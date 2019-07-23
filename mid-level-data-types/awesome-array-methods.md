---
description: >-
  Arrays are my very favourite data structure in JavaScript. Let's see why by
  exploring precisely what makes them great.
---

# Awesome Array Methods

I wish every data structure in JavaScript was as cool as Arrays. No, really, I'm not being hyperbolic or sarcastic, and I'm going to prove it. 

{% hint style="warning" %}
Most array methods use _functions_ so you should probably head on over to [Understanding Functions](../functions.md) before you read this page. I promise it'll be much easier once you've done that!
{% endhint %}

## Array.map\(\)

Array.map\(\) is used to iterate over an array and return a new array which contain values that each loop iteration returns. map\(\) takes a single argument which must be a [function](../functions.md). This function will be called with 3 different arguments: `currentValue` , `currentIndex`, `inputArray`. Mostly in the wild you'll only see the first argument being used \(the current value in the array for this loop iteration\), but you might find the other 2 values... useful. 

Let's put all this into a concrete example that makes sense. Let's say I have an array of words that I want to put in all caps. To modify my array, I have to loop through it, which of course can be done with some archaic method using temporary variables and for...i loops \(eww\): 

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

But by golly, that's a lot of code for something that can so easily be done not only without an intermediary function but also with ONE SINGLE LINE OF CODE: 

```javascript
const startArray = [ 'bleh', 'foo', 'MoOoO', 'supercalifrag' ];

const upperArray = startArray.map( word => word.toUpperCase() );
```

No isn't that nicely short & sweet? Can you think of anything else that map\(\) can be used for?

## Array.filter\(\)

Array.filter\(\) is used to _remove things you don't want_ from an array, by... well, by filtering them out. It will return a new array where some array elements have been removed. Which elements? They're determined by a function - filter\(\) takes a function which needs to return a truthy or falsy value \(see the [Conditions ](../conditions.md)page to know what that means\) - truthy values keep the element in, falsy values throws the element in the garbage and you never see it again. 

As a concrete example, let's say I want to only keep values that are _odd_ in an array, and eliminate any _even_ number. We'll use a tiny bit of mathematics to do this, more specifically the _modulo_ function, which in JavaScript is used with `%`. Basically, if you `% 2` a number, it'll return 0 \("falsy"\) if it's even, 1 \("truthy"\) if it's odd. Simple, right? Let's do this!

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

Let me leave you with a last super useful trick that's a common enough question to warrant its own little example. You can filter out `null` and `undefined` values easily from an array using one of JavaScript's built-in function, `Boolean()`. Boolean\(\) will return an actual true/false value, and it can be used directly in a filter\(\) function [as described in the functions page](../functions.md#lambda-anonymous-functions). Here it is: 

```javascript
const noEmpties = myArray.filter(Boolean);
```

You can of course use any function that expects an input and returns a boolean value here, whatever that function is. I'll leave the rest to your imagination for now.

{% hint style="info" %}
The Boolean function returns false on empty strings `''` or the number `0` so be careful when you use it!
{% endhint %}

## Array.reduce\(\)

\[ TBD cuz lazy right now \]

## Array.sort\(\)

\[ TBD cuz lazy right now \]

## Array.find\(\)

\[ TBD cuz lazy right now  \]

## Array.every\(\)

\[ TBD cuz lazy right now \]

## Array.includes\(\)

\[ TBD cuz lazy right now \]

