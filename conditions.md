---
description: >-
  Let's talk about conditions, how to use them, how to combine them, and all
  that jazz!
---

# Understanding Conditions

A "condition" is a way to make certain parts of your code run _only_ when specific criteria are met. When using conditions, you're creating a new block of code that runs, _or not_, depending on whether the condition returns a `true` or `false` value. 

Let's look at a very basic script that uses a condition. 

```javascript
const name = "Joe";

if(name === "Bob") {
  console.log("Hi Bob!");
} else {
  console.log(`Hello ${name}.`);
}
```

So here we have a condition that checks: "If the name is EXACTLY Bob, say hi to bob. Otherwise, say hi to whoever the hell this is". As a reminder, that fancy thing that says "hello, name." is a [Template Literal](template-literals.md). 

### Conditions work with Booleans

A condition will always expect something that can be considered a Boolean value, that is to say, it evaluates to "true" or "false". It also will accept what we call "Truthy" and "Falsy" values which... Well, basically _everything_ in JavaScript is truthy or falsy. 

Here's a few examples of things that can return literal `true` and `false`: 

* Loose Equal operator: `==` compares two values that can be of different types but, when compared with ==, have the same value. For example, `1 == "1"` returns `true`. 
* Strict Equal operator: `===` compares two values that must be of the same type. `1 === "1"` is `false`, but `1 === 1` is `true`. 
* Math operators such as `>` , `<` , `>=` and `<=`. 
* Boolean return functions: a whole lot of functions will return booleans of true and false. For example, [String.startsWith](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith) , [Array.includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes), [Map.has](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/has), [isNaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN)... You'll notice that in those documentation pages, you can see that the **Return Value** is defined either as `true` or `false`, or as `Boolean`. 

As for truthy/falsy, the rule is actually pretty simple. Here is an exhaustive list of Falsy values: 

* `null` and `undefined`
* `0` \(the number 0\)
* Empty strings including `""`, `''`, empty template literals.
* `false` , of course. 
* `NaN` \("NotANumber"\)

Literally every single other thing in JavaScript is considered truthy. This includes functions and arrays, positive and negative numbers, Objects and Arrays \(yes, even the empty ones\).

Here's a couple of examples: 

```javascript
if(1 > 3) // false
if([]) // true
if(parseInt("Blah")) // false
if(0) // false
if("true") // true
if("false") // true. This isn't a boolean value it's a string!
```

### Inverting Booleans and Conditions

In the "Loose Equal" and "Strict Equal" operators above, I used `==` and `===` , to indicate that something should be equal. But what if I want it the other way around? How do I make something **NOT** equal? Well, anytime you think "not" in JavaScript, replace that with `!` in your code and you'll end up with the opposite boolean. To simplify this to the extreme: 

```javascript
!true // this equals false
!false // this equals true

!0 // true
!"Blah" // false
!undefined // true
```



