# Template Literals

Strings are all well and good, but sometimes they're a little awkard when wanting to mix strings and variables. Ever seen something like this code? 

```javascript
console.log("There are " + getCount() + " things in the " + getName() + " collection");
```

Template literals are here to save the day. Here's the same string, using them: 

```javascript
console.log(`There are ${getCount()} things in the ${getName()} collection`);
```

There are 2 things you will notice here. First, template literals don't use single or double quotes, but rather use ````` which are called "backticks" \(for you french language speakers, it's an "accent grave"\). The second, is that any variable or function is called using the ${} syntax \(they're called "placeholders"\). 

Template literals should _only_ be used if you're misxing strings and variables, or if you're using tagged templates \(see below\). Since they're _processed_ strings, it means JavaScript evaluates it and that takes extra time. This means, the following examples are not only bad, they're also ridiculous. Most people will just scream at you if you do this: 

```javascript
console.log(`${variable}`); // please don't!
console.log(`This is just a string, why are you doing this?`);
```

### Nested Templates

Since you can use javascript expressions in placeholders, you can nest one template literal inside another. This simplifies complex code and can remove the need for temporary variables. In this example, we'll see how you can actually do a loop inside a template literal that contains a template literal. LITERALCEPTION!

```javascript
const commands = commandList.map(comm => `Name: ${comm.name}, uses: ${comm.uses}.
    Aliases: ${aliasList.get(comm.name).map(alias => 
      `Name: ${alias.name}, uses: ${alias.uses}`).join(" ; ")}`).join("\n");
```

Now... this seems complicated, because nested templates are definitely not that simple, but I hope you get the idea, even if the code highlighting somewhat screwed the pooch on the colors here. The basic idea is that you can have functions inside of your template literal's placeholders that themselves contain template literals, and this works as one would expect. 

### Tagged Templates

One other use for template literals beyond mixing variables and strings, are "tagged templates" which are essentially a function applied to a template literal. These functions are directly applied to modify the result of the template literal _in place_, meaning you don't have to call a function and return a value.

```javascript
// a real basic example
const result = myFunction`This is a template literal with ${variables} and stuff`;
```

However, wanting to write this section, I realize that I can't possibly explain this better than the [MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) can. Check the "Tagged Templates" section of that page \(and/or read the whole thing, because it's a great documentation piece!\). 

