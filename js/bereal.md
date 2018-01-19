# Let's be real here ...

In reading more and more of these questions, I am finding some questions where there is some historical significance or relative importance to the overall community, but knowing the answers to these colloquial questions does not, in any way, establish your personal creditability or skill level as a front-end developer.

I would also argue that some of these questions should be removed from this list altogether. So, if interested, read on. If not, ignore and get onto the more important things in life.

#### What is the difference between == and ===?

I am just going to say this, if you don't know this answer immediately, then you need to crack open your JavaScript 101 book and start over.

In JavaScript there are a series of [basic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators), within this list of operators are [comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators).

That being said, the `==` comparison operator means that something is equal to each other, even if their value is made equal via type coercion.

```js
1 == 1 / true
'1' == 1 / true
```

Now, `===` is a comparison operator that will evaluate value and type.

```js
1 == 1 / true
'1' === 1 / false
```
