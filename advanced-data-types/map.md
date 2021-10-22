---
description: Who do you ask when you don't know which way to go? The Map!
---

# Map

I like to consider that a Map is a "better version of objects", though that's not completely true. Let's take a look at what they are, how they work, and what advantages there are to using Maps.

To use a more or less proper terminology, a Map is an unordered key/value pair storage, where each "key" refers to a "value" stored in Map. You could sort of think that the key is just like a variable, and the value is whatever you assign to that variable. As usual I'm probably making this sound more complicated than it is, so just keep on reading and I'm sure you'll get it :D

## Creating a new Map

Maps are created by instanciating a new class of the Map class. If this sounds like goobledygook to you, take a quick look at Understanding Classes, but if you don't care, just carry on, it's not super important ;)

```javascript
// Create a new, empty Map
const myMap = new Map();
```

As with pretty much any data type, you can create a new Map with existing data. The data needs to be something called an "Iterable" which essentially means "something that can be looped on". The most straightforward way is an array which contains arrays, each with a key/value pair, as such:

```javascript
// Create a new Map from an array
const newMap = new Map([
    ['a', 'alpha'],
    ['b', 'bravo'],
    ['c', 'charlie']
]);

// If you want to be fancy, you can do it from an object too!
const mapFromObject = new Map(Object.entries({
    a: 'alpha',
    b: 'bravo',
    c: 'charlie'
}));
```

Ok so now you have a Map, what can you do with it? Let's see the main ways in which you can interact with it.

## Setting Values

You can set a value to a Map using the `set(key, value)` method:&#x20;

```javascript
// Let's start with an emtpy Map
const myMap = new Map();

myMap.set('a', 'alpha');

// Remember you can use *any* primitive type as a key
myMap.set(1, "one");
// Yeah, even arrays...
myMap.set(['blah'], { values: 'can also be what you want' });
```

## Getting Values

Maybe it's a bit obvious, but getting value from a Map uses... `get(key)`. I know, I know, super fancy, right?

```javascript
const something = myMap.get("a"); // "alpha"

console.log(myMap.get(['blah']));
// prints { values: 'can also be what you want' }
```

## Deleting Values

The easiest way to delete a value from a Map, is simply to use the `delete(key)` method. So, `myMap.delete("a")` would delete the key "a" with the value "alpha" in the above Map.&#x20;

You can also completely clear any data from a Map to reset it to zero, by using `clear()`. Watch out, you can't "undo" things in a Map so when data is deleted, it's gone!

## Iterating over data

An important part of a healthy data structure is the ability to loop over that data. That is to say, you want to be able to act upon every item inside your Map. Here's a couple of very useful properties that let you do that!

To iterate over only the keys, you can use the `keys()` method. This returns an array of all the keys (but not the values) in your Map:&#x20;

```javascript
const mapKeys = myMap.keys();

for (i = 0; i  < mapKeys.length; i++) {
    console.log(`Key ${mapKeys[i]} has value ${myMap.get(mapKeys[i])}.`);
}
```

If you want the values instead, you can use `values()`. Yes, quite remarkably predictable, isn't it?&#x20;

Lastly, you can loop over both the keys and arrays in two different ways, `forEach()` and `entries()`. `Map.entries()` will return an array of key/value pairs in their array (so, just like what's used to create a new Map in the first place!), so you can loop over that if you want. The easiest , however is the forEach loop:&#x20;

```javascript
// Foreach takes a callback function that provides the Key and Value
// Watch out though, they're "reverse" order, with the value first!)
myMap.forEach( (value, key) => {
    console.log(`Key ${key} has value ${value}.`);
});
```

> Callbacks and functions are explained in the [Understanding Functions](../functions/) page.
