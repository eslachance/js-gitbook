# Pure Functions and Side-Effects

In programming in general (this is not limited to JavaScript itself), there is a concept of a function that is "pure", which is the same as saying this function does not have any side-effects. What this means is that the function will not, and cannot, affect any variable or data or the environment around it.&#x20;

It also means one other important thing: that this function, given the same _arguments_, will **always** return the same _result_. Pure functions don't affect _or rely on_ information outside of the function itself - everything it needs is given to it via its arguments.

Let's put this as 2 clear cut examples. First, the wrong one : let's see the _impure _function:

```javascript
let a = 5;

const impureAdd = (addValue) => {
  a = a + addValue;
  return a;
};

console.log(impureAdd(10)); // 15

console.log(a); // 15
```

So what's going on here? Inside the function, the value of `a` is being modified by the function itself. The function relies on `a` being defined first, and also has the _side-effect_ of mutating (changing) the value of `a` outside of itself. This means that if anything later on is relying on the value of `a`, maybe that value is correct, maybe it's wrong, who knows? That's a side-effect.

Now let's go ahead and take a look at a _pure_ function instead:&#x20;

```javascript
const a = 5;

const add = (num1, num2) => {
  return num1 + num2;
};

console.log(add(a, 10)); // 15
console.log(a); 5
```

It's pretty clear from this example that now the add function has no side effect. It takes 2 arguments, returns them as-is, and never affects anything around it.

Importantly, a function can have side-effects that don't directly relate to its arguments and return values. Indeed, this is a _very bad_ function with a side-effect that will potentially break any code in your project or its dependencies:

```javascript
// Never do this!
const setupProject = () {
  // poluting global is not good
  global.projectName = "My Project";
  // extending core javascript prototypes is horrible!
  Array.prototype.sample = function(){
    return this[Math.floor(Math.random()*this.length)];
  }
}
```

The above does 2 different things which affect something outside of itself, and thus, is a function with two _side-effects_.&#x20;
