---
description: >-
  The very basics of JavaScript: How to save something inside a little token
  contained called a "variable"!
---

# Variables

Let's assume for a second that you've never heard of JavaScript, you don't know the terminology or the syntax, you're basically starting from scratch. This page presents the most basic stuff you'll encounter. 

### Variables

A _variable_ is a "container" for data, that can change \(which is why it's "variable", get it?\). Variables are _declared_ by giving them a _variable name_, as well as _value_ \(or "content" or "data"\). There are 3 ways to declare a variable: 

```javascript
// the "var" keyword is not really used anymore, but you'll still see it in older
// code. It's suggested not to use it anymore. Use let instead!
var myVariableName = "This is a string value";

// The "let" keyword defines a variable where the value and type can be changed later.
let myOtherVariable = "We can change this later";

// If you're going to define the actual value later, you can simply declare it
// without giving it a value
let changeMeLater;

// We can change the content of an existing variable by omitting the "let" keyword.
changeMeLater = "Oh cool I have a value now!"

// The "const" keyword defines a variable that can't change type but, in the case
// of objects and arrays (see "Data Types" below) can be modified. You'll see this
// better in context later on.
const actuallyConstant = "I cannot be modified";
actuallyConstant = "This will fail";

const notReallyConstant = { blah : "foo" };
notReallyConstant.blah = "meh";
notReallyConstant.thing = "thing2";
```

Let's break down a single line here to look at the syntax: 

* `let/var/const` are JavaScript _keywords_ that triggers a new variable to be created. 
* The _variable name_ also called _identifier_ is created. There are some limitations to identifier names, see this page for more details. 
* `=` is an _operator_ that means "insert whatever comes after me, into the variable before me" 



