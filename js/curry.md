# Can you give an example of a curry function and why this syntax offers an advantage?

Curry functions are all the rage lately (or at least at the time of writing this). So, what is a curry function? Simply put, it is only a 'style' of writing a function as there is NO official curry function spec in JavaScript. The drive behind using curry functions is to try and make a complex closure style function simpler to follow.

What does this look like? For starters, let's use a really simple example. Start by creating a standard function with a single argument. Then, the return of that function is another function with another single argument. Inside that function, we will do a simple return that combines the values of the first two arguments.

```js
function foo(a) {
  return function(b) {
    return a + b;
  }
}
```

When looking at this closure, while we pass in an argument for `a`, the return of this function is the anonymous function within.

```js
// execute
console.log(foo(5));


// return
function (b) {
  return a + b;
}
```

To complete this function, we could use a closure pattern ...

```js
const bar = foo(5);
console.log(bar(10)) // 15
```

Or, we could use a curry pattern. What currying allows us to do is reference the function and pass in the two arguments in a single execution by paring up the parens `()`.

```js
const bar = foo(5)(10);
console.log(bar) // 15
```


## How I would answer this in an interview

To answer the first part of the question, I wouldn't give any more complex of an answer then that presented here. Unless you really understand their use case and fee like showing off. That's all on you.

For the second part, the advantage that this syntax offers, The obvious is a developer's ability to breakdown complex functions and allow for nested functions to be returned as a function and be assigned to other variables. The curry style function helps make the code easier to follow.

Another advantage is that this syntax encourages users to follow a functional programming style versus the creation of methods more commonly seen on OOP style JavaScript.
