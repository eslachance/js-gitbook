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

if( name === "Bob" ) {
  console.log("Hi Bob!");
} else {
  console.log(`Hello ${name}.`);
}
```

So here we have a condition that checks: "If the name is EXACTLY Bob, say hi to bob. Otherwise, say hi to whoever the hell this is". As a reminder, that fancy thing that says "hello, name." is a [Template Literal](template-literals.md). 

### Conditions are a Scope

I haven't really touched yet on "Scopes" in this page, but here's an important point about conditions: they create a new scope. What that means is that if you, for instance, define a variable inside a condition, it will not be available outside that condition: 

```javascript
if ( thingIsTrue ) {
  const blah = "Foo";
}
console.log(blah); // undefined
```

Keep that in mind when writing your conditions. 

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
if ( 1 > 3 ) // false
if ( [] ) // true
if ( parseInt("Blah") ) // false
if ( 0 ) // false
if ( "true" ) // true
if ( "false" ) // true. This isn't a boolean value it's a string!
```

### Conditions can be Inverted

In the "Loose Equal" and "Strict Equal" operators above, I used `==` and `===` , to indicate that something should be equal. But what if I want it the other way around? How do I make something **NOT** equal? Well, anytime you think "not" in JavaScript, replace that with `!` in your code and you'll end up with the opposite boolean. To simplify this to the extreme: 

```javascript
!true // this equals false
!false // this equals true

!0 // true
!"Blah" // false
!undefined // true
```

### Conditions can be Combined

So what if you need to combine two conditions together? Of course you could do something like:

```javascript
if ( thing ) {
  if ( otherThing ) {
    doSomething();
  }
}
```

Looks pretty ugly, doesn't it? Well, there are ways to combine these things into a single condition, by using the AND \(&&\) and OR \(\|\|\) operators. 

* `&&` means "**BOTH** must be true for the condition to return true"
* `||` means "**EITHER** can be true for the condition to return true"

The above can thus be written simply with: 

```javascript
if ( thing && otherThing ) {
  doSomething();
}
```

Combined conditions are read from left to right by default, unless you override that order with more parentheses. If you recall high school math, you might remember a little thing called the "Order of Operation", or "PEMDAS". In terms of conditions \(not math\), the important thign to remember is that the P is first, which means that parentheses always, _always_ get parsed first.

Take a look at this more complex example: 

```javascript
if ( ( true && false ) || ( false || true ) ) {
  // this will run
}
```

So what's happening here? 

* First,  `( true && false)`  is evaluated. It returns `false` because the AND operator requires both to be true.
* Then ,  `( false || true )` is evaluated. It returns `true` because the OR operator allows either to be true.
* So we're now left with  `(false || true )` which of course returns true because, read right above.
* In the end, `if(true)` obviously will let the code inside the condition run. 

{% hint style="warning" %}
Warning: While you might expect something like `if ( thing === 'one' || 'two' || 'three' )` to work... it doesn't. Because conditions convert everything to truthy/falsy values, you end up with `if( true || true || true)` or `if ( false || true || true)` and in both cases, the condition will run. There are ways around this sort of problem, such as Array.includes\(\), which you'll find in [Awesome Array Methods](mid-level-data-types/awesome-array-methods.md).
{% endhint %}

One last note: conditions are always read left to right, and some optimization can be gained by understanding a very cute fact: _**If you have a bunch of OR operators, the first true value will stop the chain completely**_. What I mean by this is that you should always order your conditions, if at all possible, from "most common" on the left, "less common" on the right. You should also make a check that's more CPU-intensive appear at the end of a condition chain, if you can avoid it with another condition. 

Let me explain with some code: 

```javascript
const veryIntensiveCheck = () => true; // imagine this takes 30 seconds to run.
const simpleCheck = () => true; // imagine this takes 10ms to run.

// This condition will take 30 seconds to return a value
if ( veryIntensiveCheck() || simpleCheck() ) {
  return true;
}

// This condition will return almost immediately after 10ms
if ( simpleCheck() || veryIntensiveCheck() ) {
  return true;
}
```

So, to re-iterate, the second version is faster because in a combined OR chain, if ANY of the condition is true, we know the entire chain should return true, so what's the point of even checking the rest? So it doesn't!

### Conditions can be Ternary

Ooooooh ternary conditions. A complicated word for such a simple and awesome concept. So in [Conditions are a Scope](conditions.md#conditions-are-a-scope) , we saw that you can't define a variable inside a scope and use it outside. There's a way to get around this, which looks something like:

```javascript
let value;

if ( thingIsTrue ) {
  value = "yay";
} else {
  value = "booh";
}
// value works here
```

But... this is ugly as hell, is it not? It also means that in some complex code where you use many different variables, you might end up with a metric crapton of variables specifically created with the purpose of holding a temporary value, and being reassigned a new value right away. This will hurt both your performance and your brain, so let's start by making this a bit simpler, using the Ternary operator. Its use is super simple: 

```javascript
(condition) ? trueValue : falseValue;
```

A ternary always _returns_ either the true or false value, which means it can be used in many different interesting ways. First off, it can simplify the example above: 

```javascript
const value = thingIsTrue ? 'yay' : 'nay';
```

But why even have this variable in the first place? As with a lot of things that return a value, they can be used directly in many ways.

* You can return them : `return someFunction() ? 'It Worked!' : 'Failure in function';`
* You can use them in objects: `{ value: check(blah) ? 'blah' : 'default' , otherValue: 'meh' }`
* You can even use them in functions like Array.map! `myArray.map(val => isOdd(val) ? 'odd' : 'even')`

With this in mind you should have a better time writing shorter, more elegant code when dealing with simple values.

### Condition Operators Overload

I'll be honest, I'm pulling this terminology out of my ass, but I haven't really seen a definitive name for this technique and those that exist are weak. It's sort of a different way to define a variable in a similar fashion to the Ternary above, but if you only have a `true` or `false` value and not the other. Let's see what I mean: 

```javascript
const myName = input.name || 'No Name';
const text = hasDetail(input) && `User Message: ${input.message}`;
```

So what's happening above, and why can we use this? It has to do with the chaining that was discussed in the Combining portion of this page. Simply put, when JavaScript sees a _false value on the left_ operand followed by `||` , it continues down the chain, and will return the value on the right. If it sees a _true value on the left_ followed by a `&&` it will also return the value on the right.

This means that in addition to knowing that _an OR condition chain will stop being evaluated on the first truthy value it finds_, we also know that in any condition chain, _the last value is always returned to the calling code_. 

There are some pretty damn nifty tricks you can do when you understand these 2 things correctly, but for the time being, I feel I've already filled your head with too much goobledygook so we'll leave it at that. Have fun conditioning your brain!

