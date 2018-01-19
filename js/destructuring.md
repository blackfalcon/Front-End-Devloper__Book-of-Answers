# Can you give an example for destructuring an object or an array?

The destructuring assignment syntax is a completely new concept to JavaScript via the ES6 specification. Just looking at it, I feel that it makes little sense. But once you understand what it is trying to do, it all falls into place.

> The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

First, let's talk about the syntax. To the left you start with your declaration, be it `var`, `const` or `let`. Then you have your object or array literal syntax. Last, you point to the object or array you are destructuring.

What needs to be understood first is that the elements that will go into the object or array literal syntax is what will be unpacked from the original object or array and assigned to individual variables.

```js
declaration { ... } = object

or

declaration [ ... ] = array
```

Why would you use this? The main reason for the destructuring syntax is, once again, for the purpose of having less procedural code in favor of more declarative code. Like I said, once you understand the syntax you will come to look at the destructured expression and quickly understand what it is doing.

## Destructuring arrays

The first object we will look at destructuring is the array. The following is a quick abstract example of how to destructure an array. First, we have some function that is returning whatever is passed into it. Then we have an array of many things, including that function.

```js
const foo = (arg) => {
  return arg;
}

const arr = [1, 'alpha', foo, 1, 2, false, 4, true];
```

To destructure this array we could, for example, take the first item and apply that value to a new variable of `num`. Then the second, bind to the variable of `str`. And last, bind `foo` to `funct`.

```js
const [num, str, funct] = arr;
```

Having done that we can now console log out the values of these new variables.

```js
console.log(num); // 1
console.log(str); // "alpha"
console.log(funct('yay')); // "yay"
```

But what of the remainder of the array? With the destructuring syntax, we can actually grab the remaining items in that array via the spread `...` syntax and simply place that into another array.

```js
const [num, str, funct, ...leftOvers] = arr;

console.log(leftOvers); // [1, 2, 3, 4, 5]
```

## Destructuring objects

Much in the same way that pulling values out of an array is a repetitive task, the same can be said for pulling values from an object. And again, destructuring can help. The following example illustrates the basic concepts around destructuring an object. What is important to understand is, unlike arrays, object destructuring is based on the object's keys.

In the following example, I have a simple object that describes a new television.

```js
const obj = {
  manufacture: 'Samsung',
  size: '50-inch',
  resolution: '4K Ultra HD Smart LED',
  price: 527.99
}
```

Let's imagine that we have a function that consumes this object and creates a series of variables from it. These variable declarations may look like this.

```js
const manufacture = obj.manufacture
const size = obj.size
const resolution = obj.resolution
const price = obj.price
```

That's not too bad, but given the power of destructuring, we can actually do the same thing in one line. And remember, we need to use the same key name as it appears in the object in order to make the connection. But this also allows us to destructure in any order, unlike how arrays work.

```js
const {manufacture, price, size, resolution} = obj;
```

We can even destructure an array contained within an object. Let's update our object to have an array of outlets where this television can be bought.

```js
const obj = {
  manufacture: 'Samsung',
  size: '50-inch',
  resolution: '4K Ultra HD Smart LED',
  price: 527.99,
  retailers = ['Amazon', 'BestBuy', 'Costco']
}
```

Even though this array is within an object, we would still use the `[]` syntax to destructure the data and reference the specific object and key.

```js
const [one, two, three] = obj.retailers;
```

Now let's imagine that we have the URLs for each of the product pages on the retailer's sites.

```js
const obj = {
  manufacture: 'Samsung',
  size: '50-inch',
  resolution: '4K Ultra HD Smart LED',
  price: 527.99,
  retailers: ['Amazon', 'BestBuy', 'Costco'],
  purchaseOnline: {
    one: 'http://www.amazon.com',
    two: 'http://www.bestbuy.com',
    three: 'http://www.costco.com'
  }
}
```

Then to quickly and easily get these values, we could use the following code. Note that since these are object keys we are using the `{}` syntax.

```js
const {one, two, three} = obj.purchaseOnline;
```

## How I would answer this in an interview

In an interview, Keep It Simple Stupid! Either example shown here would be great, just don't get too fancy with your example. Illustrate that you understand the fundamental explication of this assignment syntax and you will go far!
