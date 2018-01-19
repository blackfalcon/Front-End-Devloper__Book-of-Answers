# What's the difference between .call and .apply?

The `.call()` and `.apply()` methods pretty much do the same thing, it's just that the `.call()` method operates on arguments and the `.apply()` method operates on argsArray. What does that mean? Here are the specs of both methods. What's consistent is the use of thisArg.

```js
// the call() method
function.call(thisArg, arg1, arg2, ...)

// the apply() method
func.apply(thisArg, [argsArray])
```

## The call() method

The `.call()` method is defined as the following:

> The `call()` method calls a function with a given `this` value and arguments provided individually.

What does that mean? To put it simply, the `.call()` method will call a function that consists of a reference to `this`, but is void of context. Using this method we can set the scope of `this` to an object we want to use the values of, and then apply the arguments to the function. I like Mad Libs and they make really great examples, so let's imagine that we have a program that will allow you to create a simple Mad Lib that has two parts to do this. One is to use a pre-defined object of words, and the other is to supply two arguments for additional words.

Here are our pre-defined objects.

```js
const madLibsOne = {
  adj: 'slimy',
  verb: 'wiggle',
  noun: 'Texas',
}

const madLibsTwo = {
  adj: 'purple',
  verb: 'rain',
  noun: 'dove',
}
```

Then we have a function that will have the `this` value. This will print out our Mad Lib. In this function we see that there are references to `this` properties, but there is no context of `this` so these will return `undefined` if we try to run this function alone and simply add the two word arguments.

```js
function printMadLib(nounOne, nounTwo) {
  return `Our school cafeteria has really ${this.adj} food. Just thinking about it makes my stomach ${this.verb}. The hamburgers tastes like ${this.noun}. My friend Dave likes the ${nounOne} and thinks that it's made of ${nounTwo}.`
}


printMadLib('frog', 'rocks'); // "Our school cafeteria has really undefined food. Just thinking ..."
```

Using the `.call()` method we can use the same function, but reference the data from one of the pre-defined object and get a better return.

```js
printMadLib.call(madLibsOne, 'frog', 'rocks'); // "Our school cafeteria has really slimy food. Just thinking about it makes my stomach wiggle. The hamburgers tastes like Texas. My friend Dave likes the frog and thinks that it's made of rocks."

printMadLib.call(madLibsTwo, 'frog', 'rocks'); // "Our school cafeteria has really purple food. Just thinking about it makes my stomach rain. The hamburgers tastes like dove. My friend Dave likes the frog and thinks that it's made of rocks."
```

What this example illustrates is how we can execute a function, pass in the reference to the `this` object and then satisfy the arguments of the function for the desired output. The power this gives us is the ability to abstract functions/methods away from objects, reduce complexity and increase flexibility.

## The apply() method

The `.apply()` method is defined as the following:

> The `apply()` method calls a function with a given `this` value, and arguments provided as an array (or an array-like object).

What does this mean and why is this different from `call()`? The syntax of this function is almost identical, but the main difference is that `call()` accepts an argument list, while `apply()` accepts an array. Let's refactor the previous example and instead of passing in the two additional nouns as individual arguments into the function, we can pack those into an array and then pass that array into the `.apply()` method along with the object reference.

```js
const thisArray = ['farmer', 'car'];
const thatArray = ['television', 'fireplace'];

printMadLib.apply(madLibsOne, thisArray);
printMadLib.apply(madLibsTwo, thatArray);
```

And the return we get in the console is the following:

```js
"Our school cafeteria has really slimy food. Just thinking about it makes my stomach wiggle. The hamburgers tastes like Texas. My friend Dave likes the farmer and thinks that it's made of car."
"Our school cafeteria has really purple food. Just thinking about it makes my stomach rain. The hamburgers tastes like dove. My friend Dave likes the television and thinks that it's made of fireplace."
```

## How I would answer this in an interview

So yes, the `call()` and the `apply()` methods do exactly the same thing. They easily bind an object to a function and designate the value of `this`. What makes them different? It's their application of the additional arguments for the function. `call()` uses individual arguments while `apply()` allows you to pass in an array.

Bonus answer: Because it's JavaScript we can totally hack on this. We can use the `call()` method and pass in an array if we use the `spread` parameter syntax.

```js
printMadLib.call(madLibsOne, ...thisArray)
```

Yeah, that works.
