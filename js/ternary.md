# Why is it called a Ternary operator, what does the word "Ternary" indicate?

First I will answer the second part of the question. The word 'Ternary' indicates something that is composed of three items. Ok, so what does that have to do with JavaScript and what is a Ternary operator? Answer ... it's an `if()` statement.

The structure of a common `if()` statement looks like the following.

```js
if ( ... ) {
  ...
}
```

The conditional (ternary) Operator is not new with ES6, but has been recently popularized with new emphasis on succinct code patterns. The syntax is surprisingly simple. Notice how there are three (ternary) parts, the condition and the two expressions.

```js
condition ? expression1 : expression2
```

For the `condition`, simply pass in what you want to evaluate. This would be the same thing you put inside the `()` parens in an `if()` statement. E.g. `a === b` or `i < x`.

Next, `expression1` represents the return of `conditions` if true, leaving `expression2` to be the return if `condition` is false. See the following example for a standard `if()` statement with it's simplified ternary version.

```js
var a = 10;
var b = '10';

// if() statement
if (a === b) {
  alert('winning')
} else {
  alert('not equal')
}

// ternary operator
a === b ? alert('winning') : alert('not equal')
```


## How I would answer this in an interview

This question is really addressing your knowledge of JavaScript terms and modern syntax. to answer this question, I wouldn't go into a lot of detail in regards to how this is used, I would simply say, "_It's called a Ternary operator because it is made up of three parts, the condition and the two expressions. Ternary means, something that is composed of three items._"
