# What are the benefits of using spread syntax and how is it different from rest syntax?

This is a great question, but in order to answer it, you need to understand how this syntax works.

## The spread and rest parameter syntax

In common function example there is a clear 1:1 parsing of the input parameters and the arguments within the function, and in most cases, this will not be an issue. In the cases where the input is more variable, this syntax can be very limiting. For example, the following code illustrates that by passing in additional parameters, this has no effect on the output, good or bad.

```js
function sum(num, num2, num3) {
  return num + num2 + num3
}

const foo = sum(1, 2, 3, 4, 5, 6) // 6
```

It is here where the `spread` and `rest` parameter syntax, `...`, can help solve this problem. While the `...` syntax is the same, their applications are clearly different.

> The rest parameter syntax allows us to represent an indefinite number of arguments as an array.

> Spread syntax allows an iterable such as an array expression or string to be expanded ...

What does this mean? In the case of the `rest` parameter syntax, an unrestricted number of argument inputs become a single array parameter.

Looking at the previous example, the `rest` parameter syntax can be used to replace the individual parameters. As stated, this will turn the input into an array and as a result the inner workings of the `sum()` function needs to be updated to loop through the values of the input array.

```js
function sum(...args) {
  let answer = 0
  for (let i=0; i<args.length; i++) {
    answer += args[i]
  }

  return answer
}
```

With this update, the new `sum()` function can accept an unlimited number of parameters and output an answer.

```js
const args = sum(10, 13, 4, 7, 12) // 46
```

Given that the `sum()` function has been updated with the `rest` syntax and the input parameters are now an array, one could assume that an array could be pass into the `sum()` function. This assumption would be incorrect as this would be considered a single parameter and this function would return `0` plus the array.

```js
const array = sum([10, 13, 4, 7, 12]) // "010,13,4,7,12"
```

As a 'dirty hack', developers started using the `apply()` method on the Function as this allows for arguments to be passed in as an array. This is a 'dirty hack' is because of the use of `null` in the function in place of the `thisArg` parameter in the method.

```js
// Syntax
// func.apply(thisArg, [argsArray])

const applyArray = sum.apply(null, [10, 13, 4, 7, 12]) // 46
```

The `spread` parameter syntax, on the other hand, can avoid the 'dirty hack' altogether. The `spread` parameter syntax differs from the `rest` parameter syntax because of its direct application of an array as a parameter when executing a function. This syntax is illustrated in the following example.

```js
const spreadArray = sum(...[10, 13, 4, 7, 12]) // 46
```

A combination of these parameter syntax types and this function, inputs are virtually unlimited.

```js
const spreadArray = sum(...[10, 13, 4, 7, 12], ...[1, 2, 3], 100, 50, 50, ...[1, 2, 3]) // 258
```

Don't forget, the `spread` parameter syntax allows `an iterable such as an array expression or string` to be used. That means, using the `spread` syntax one can pass in a string and it will be iterated over like an array.

```js
const spreadArray = sum(...[1, 2, 3], ...' = sum total') // "6 = sum total"
```

## How I would answer this in an interview

The benefit of using the `spread` syntax is having the ability to pass in an array as an argument to a function. Without this syntax you would need to hack on the function's argument, e.g. using the `apply()` method.

The difference between the two is in its application. The `spread` syntax is applied to the execution of a function while the `rest` syntax is used in place of parameters in the function definition.
