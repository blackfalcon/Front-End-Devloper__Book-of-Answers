# Explain how `this` works in JavaScript

IMHO, this is a HUGE question to drop on someone in an interview. But, it is a concept that if you don't understand, you will find it very hard and very confusing to program anything in JavaScript.

Simply put, `this` is a contextual reference pertaining to the action being performed or the data being presented. The `this` keyword can be used to access values, methods and other objects that are context specific.

There are 5 ways that a `this` will get it's value

1. Within the context of a function
1. Within Methods and Objects
1. Within a Constructor
1. When a function is invoked via `.call()`, `.apply()` and `.bind()` methods
1. What about the `=>` function?

Trust me, the answer to this is not short and there are a ton of resources out there to reference between articles and video tutorials. The following examples will try to illustrate the answers as easily as possible.


## Within the context of a function

One of the simplest concepts of `this` that we can start with is how `this` is contrived from an event. And the event, in this context, is any interaction a human user would have with your application. Be it either a click, tap or mouse gesture.

In this example HTML there are three DOM elements all with the same class name. By clicking on each DOM element, the intention is to have only that element change text. Without the concept of `this`, solutions would mean having to use unique IDs per DOM element or writing individual functions per DOM element.

```html
<body>
  <p class="changeStr">Clicking here will only change this string of text.</p>
  <p>Clicking here will do nothing.</p>
  <p class="changeStr">Clicking here will only change this string of text.</p>
  <p class="changeStr">Clicking here will only change this string of text.</p>
</body>
```

To access the DOM elements we want to place a click event on, use the following code

```js
// find all the buttons with this class
const elements = document.getElementsByClassName('changeStr');
```

Next we will write our loop that will loop through the array of DOM elements previously returned. With each loop, our code will place a click event on each element with a target of `this`.

```js
// loop through array and add the event of 'click' that will toggle a CSS class
for (let i = 0; i < elements.length; i++) {
  elements[i].addEventListener('click', function() {
    this.innerHTML = "The click event on 'this' change only this string of text!";
  });
}
```

<a class="jsbin-embed" href="http://jsbin.com/parate/2/embed?js,output">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

## Within Methods and Objects

JavaScript objects have properties. Methods are functions that, when applied, mutate or expose their data. Methods can either be written directly within the object code or applied via its prototype. It is the context of the method that is important to understand as this will have implications for the `this` property as well.

To begin to illustrate this concept, let's create a small object literal that describes `myDog`.

```js
const myDog = {
  name: 'Harley',
  breed: 'shih tzu',
  color: 'black and white',
  age: 2,
}
```

Out method will be created directly within the scope of the object to main `this` context.

```js
const myDog = {
  name: 'Harley',
  breed: 'shih tzu',
  color: 'black and white',
  age: 2,
  printObj: function() {
    console.log(`I have a ${this.color} ${this.breed} named ${this.name} who is ${this.age} year(s) old.`)
  }
}
```

What's important to notice is that the `printObj` method is bound to the `myVehicle` object directly by context. This is a very basic example of Object Oriented Programming in JavaScript.

To execute this function, we call the object and its method which will return the string we are creating.

```js
myDog.printObj(); // "I have a black and white shih tzu named Harley who is 2 year(s) old."
```

<a class="jsbin-embed" href="http://jsbin.com/regumiz/embed?js,console">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

## Within a Constructor

Constructors are templates for objects. Let's imagine that we have a program where we will be defining a lot of cars. It would take additional effort to always have to create each car object from scratch. So to templatize this process, I can create a constructor.

```js
function Automobile(make, model, color, year) {
  this.make = make,
  this.model = model,
  this.color = color,
  this.year = year
  this.printObj = function() {
    console.log(`I drive a ${this.color} ${this.year} ${this.make} ${this.model}`)
  }
}
```

It is very important to understand that `this` does NOT refer to the `Automobile` constructor itself. With each use of the `Automobile` constructor,  `this` will refer to the data associated with the new object. In the following example, I will create two new objects using this constructor.

```js
const myCar = new Automobile('Toyota', 'Tacoma', 'black', 2017);
const familyCar = new Automobile('Toyota', 'Sienna', 'black', 2008);
```

With the method inside the constructor, the objects we created will automatically inherit this method and create the scope of `this` per that new object.

```js
myCar.printObj(); // "I drive a black 2017 Toyota Tacoma"
familyCar.printObj(); // "I drive a black 2008 Toyota Sienna"
```

<a class="jsbin-embed" href="http://jsbin.com/bipecad/embed?js,console">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

## call(), apply() and bind() methods

### Invoked via the .call() method

The `.call()` method will call a function that consists of a reference to `this` but is void of context. Using this method we can set the scope of `this` to an object we want to use the values of, and then apply the arguments to the function.

Pre-defined objects.

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

Here a MadLib function to leverage the MadLibs objects. Notice the references to `this`. When running this function and only addressing the function's parameters, the references to `this` will come back as `undefined`.

```js
function printMadLib(nounOne, nounTwo) {
  console.log(`Our school cafeteria has really ${this.adj} food. Just thinking about it makes my stomach ${this.verb}. The hamburgers taste like ${this.noun}. My friend Dave likes the ${nounOne} and thinks that it's made of ${nounTwo}.`)
}
```

Using the `call()` method, we can reference the data from another object to account for `this`.

```js
printMadLib.call(madLibsOne, 'frog', 'rocks'); // "Our school cafeteria has really slimy food. Just thinking about it makes my stomach wiggle. The hamburgers taste like Texas. My friend Dave likes the frog and thinks that it's made of rocks."
printMadLib.call(madLibsTwo, 'frog', 'rocks'); // "Our school cafeteria has really purple food. Just thinking about it makes my stomach rain. The hamburgers taste like dove. My friend Dave likes the frog and thinks that it's made of rocks."
```

### Invoked via the .apply() method

Invoking `this` via the `apply()` method does the exact same thing as the `call()` method, except in how you append additional arguments. `call()` accepts arguments, while `apply()` accepts an array.

Using the same MadLibs data objects and the same `printMadLib()` function, this example illustrates how to bind the object data the same way, but instead of passing in individual arguments, you pass in an array or a reference to an array.

```js
const thisArray = ['farmer', 'car'];
const thatArray = ['television', 'fireplace'];

printMadLib.apply(madLibsOne, thisArray);
printMadLib.apply(madLibsTwo, thatArray);
```

<a class="jsbin-embed" href="http://jsbin.com/kucodif/embed?js,console">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

### Invoked via the .bind() method

Using the `.bind()` function, we are able to bind data objects to a function at will. This is a big deal as this can drastically change the outcome of the function you are working with.

Let's imagine that we have two objects, one for `doorbell` and one for `oldCar`. In each object, we have a value for the `sound` that this object makes.

```js
const doorbell = {
  sound: 'ring'
}

const oldCar = {
  sound: 'AHHOOOGAH!!'
}
```

To abstract things, let's create another object that contains the method that we can use to log the sound.

```js
const thing = {
  logSound: function() {
    console.log(this.sound);
  }
}
```

Now we have three objects, two that are specific and have value and one that is abstract and only contains a method. We can create a new variable that will reference the `thing` object that has the method of `logSound` and then `.bind()` the data for `oldCar`.

```js
let newThing = thing.logSound.bind(oldCar);
newThing(); // "AHHOOOGAH!!"
```

And what about `doorbell`?

```js
let newThing = thing.logSound.bind(oldCar);
let anotherNewThing = thing.logSound.bind(doorbell);

newThing(); // "AHHOOOGAH!!"
anotherNewThing(); // "ring"
```

<a class="jsbin-embed" href="http://jsbin.com/yiqebop/embed?js,console">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

## What about the => function?

Unlike standard functions, arrow functions do not have their own `this`. They always retain the scope from which they came. This explains their ability to maintain lexical scope when used with constructors.

Let's say for example you have a constructor that has a single method for printing out the properties of the object in the console.

```js
function Vehicle(make, model, color, year) {
  this.make = make,
  this.model = model,
  this.color = color,
  this.year = year,
  this.printObj = function() {
    console.log(`I drive a ${this.color} ${this.year} ${this.make} ${this.model}.`)
  }
}

const truck = new Vehicle('Toyota', 'Tacoma', 'black', 2018);
```

The problem comes in when you try to assign that function to another variable in an outer scope. At this point the `printObj()` function is disconnected from its original scope and thus `this` is broken.

```js
truckPrint() // "I drive a undefined undefined undefined undefined."
```

We could use the `call()` method here to address the scope issue. But using the arrow function ahead of time will save us trouble down the road.

The following example illustrates how we would update our constructor function to use a fat arrow function.

```js
function Vehicle(make, model, color, year) {
  this.make = make,
  this.model = model,
  this.color = color,
  this.year = year,
  this.printObj = () => {
    console.log(`I drive a ${this.color} ${this.year} ${this.make} ${this.model}.`)
  }
}
```

The same way we did previously, assign the `printObj()` function to a new variable, but this time the scope of `this` will follow.

```js
const truckPrint = truck.printObj;
```

Referencing the new `truckPrint()` function we no longer need to re-associate this function with object data.

```js
truckPrint() // "I drive a black 2018 Toyota Tacoma."
```

<a class="jsbin-embed" href="http://jsbin.com/fuwemuz/embed?js,console">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

## How I would answer this in an interview

`this` is an object in JavaScript that can be populated with data based on context. The real power of `this` is that you can create single functions using the `this` keyword and based on input, event, or context, and you have a lot of flexibility as to how your function will behave.

Imagine having to write a click event, or object method, without `this`? How would you do that? How much code will it take? Hint: all answers are bad and should never be discussed out loud.
