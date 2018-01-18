# Explain "hoisting"

Variable hoisting is what the JavaScript engine does in the background when it loads your code into memory. In the following example if I try to `console.log(x)` before `x` is even defined, then I get `undefined`. But after I declare the var `x` and define the value, of course `console.log(x)` will then work. This makes sense.

But if I try to `console.log(y)` without even trying to define it, I get an error. This is a little confusing?

The reason for this is simple.

```js
console.log(x); // -> undefined
var x = 5;
console.log(x); // -> 5
console.log(y); // -> error, no var declared
```

The reason behind this is that the JavaScript engine breaks apart the variable declaration and it actually looks something like this ...

```js
var x;
console.log(x); // -> undefined
x = 5;
console.log(x); // -> 5
console.log(y); // -> error, no var declared
```

So you can see that `x` actually exists BEFORE `console.log(x)`, but it doesn't have an actual value.

Just to throw a monkey wrench into this, I should point out that the new `let` or `const` variable keywords DO NOT get hoisted. For instance, in the following example we see that I am using the same code as before, but replacing `var` with `let`.

```js
console.log(x); // -> error, x is not defined
let x = 5;
console.log(x);
```

As we see here, the `x` variable was not hoisted so when we try to log `x` we get an error in the console and BOOM, you are shut down!

### What about inside functions?

Hoisting is not much different within the scope of a function. The keyword being `scope`. In the following example, `var y` is defined in the global scope. So within the scope of `function foo()` when `console.log(y)` is fired there is a valid value for that variable.

```js
var y = 10;

function foo() {
  console.log(x); // -> undefined
  var x = 5;
  console.log(x); // -> 5
  console.log(y); // -> 10
}

foo();
```

### What about functions themselves?

Functions are hoisted as well. This is a pretty powerful concept to understand as its possible to reference a function EVEN BEFORE it's been declared in the JavaScript. Take the following example. The JavaScript engine hoisted the function `hoisted()` above that of the use of `hoisted()` so it will run.

```js
hoisted();

function hoisted() {
  console.log('this works');
}
```

BUT WAIT! Anonymous functions work much like variable declarations. In the following example using an anonymous function, `var notHoisted` is declared, but not yet defined.

```js
notHoisted();

var notHoisted = () => {
  console.log('this does not work');
}
```

So calling the `notHoisted()` function prior to definition will cause an error `TypeError: notHoisted is not a function`.

If we simply move the reference to the `notHoisted();` to after the function definition, it will work.

```js
var notHoisted = () => {
  console.log('YAY! This works now!');
}

notHoisted();
```

## How I would answer this in an interview

Hoisting is a performance utility that happens when JavaScript is loaded into the engine's memory. The key to your sanity is understanding what is and what is not hoisted so that you do not run into unexpected errors when running your code.
