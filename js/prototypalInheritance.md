# Explain how prototypal inheritance works

This question is NOT for the faint of heart. Prototypal inheritance is a HUGE subject and the focus of many books and online videos. In fact, aside from you may learn from this description, I HIGHLY suggest you do some additional research on your own to ensure that you truly understand what this topic covers.

## Prototypal inheritance is an object action

To really understand prototypal inheritance, one needs to understand how an object works. The simplest definition of an object is that it has properties and methods. Take for example the `string` primitive. This data type is wrapped in the `string` object which has a single property and hosts a series of methods that help developers understand the properties of the string.

```js
const str = "Learning JavaScript can be fun and exciting!"

// string.length is a property of the string object
console.log(str.length)

// chaining together a series of methods allows for interesting ways to play with data
console.log(str.slice(0, 19).concat(' is awesome!').toUpperCase()) // "LEARNING JAVASCRIPT IS AWESOME!"
```

That being said, what are the methods in which you can create custom prototypal inheritance?

## Inheritance via constructors

A common method of creating custom prototypes is through the use of constructors. A constructor in JavaScript is simply a function that is called with the `new` operator. Each new reference to `Person` will inherit the constructor's properties and methods. In this example, by supplying default values on the parameters of the constructor, not only are the properties and methods inherited but the property's values as well.

```js
const Person = function(height = '3 feet, 1 inch', hairColor = 'green') {
  this.height = height
  this.hairColor = hairColor
  this.str = function() {
    return `This person is ${this.height} with ${this.hairColor} hair.`
  }
}

const father = new Person('5 feet, 9 inches', 'gray')
const mother = new Person('4 feet, 10 inches', 'black')

const son = ['3 feet, 6 inches', 'brown']
const child = new Person(...son)

const alien = new Person()
alien.str = function() {
  return `This alien is ${this.height} tall with ${this.hairColor} skin.`
}


console.log(father.str()) // "This person is 5 feet, 9 inches with gray hair."
console.log(mother.str()) // "This person is 4 feet, 10 inches with black hair."
console.log(child.str()) // This person is 3 feet, 6 inches with brown hair."
console.log(alien.str()) // "This alien is 3 feet, 1 inch tall with green skin."
```

As illustrated, with each instance of the `Person` constructor object, the default properties and method are always available. By passing new arguments into the parameters of the constructor function, this over-rides the defaults and outputs a custom string. But even notice how `alien.str` will override the method in the constructor function.

With each execution of the method, the function will look all the way back to its original prototype for information that is not directly applied in its instance.

## Set the inheritance of an object to a prototype object

Creating new objects that directly inherit properties from a constructor function is pretty straightforward. But there will be cases where functionality requires that a new object is created based on a previously created object and abstracting to a constructor function is overkill.

The following example illustrates two individual objects. The goal here is to combine these two individual objects into one and leverage the method in the first object.

```js
const car = {
  make: 'Toyota',
  printObj: function() {
    console.log(`${this.make} ${this.model}`)
  }
}

const myCar = {
  model: 'Tacoma'
}
```

When abstraction is not an option, using the `setPrototypeOf()` method may be an option. The purpose of this method is to bind the `myCar` object to the `car` object as its prototype.

```js
Object.setPrototypeOf(myCar, car)

myCar.printObj() // "Toyota Tacoma"
```

> Warning: Changing the [[Prototype]] of an object is, by the nature of how modern JavaScript engines optimize property accesses, a very slow operation, in every browser and JavaScript engine. The effects on performance of altering inheritance are subtle and far-flung, and are not limited to simply the time spent in Object.setPrototypeOf(...) statement, but may extend to any code that has access to any object whose [[Prototype]] has been altered. If you care about performance you should avoid setting the [[Prototype]] of an object. Instead, create a new object with the desired [[Prototype]] using Object.create().

## Objects inherit properties and methods of other objects

The previous example is a process of assigning the prototype of an object to another object in a manner that could be viewed as a backward action. It is always, as per performance reasons explained above, to keep things going in a forward manner.

In this example, the object of `car` is created using the Object Literal syntax. Using the `Object.assign()` and `Object.create()` methods, the new object `van` can be created from `car` and will directly inherit its properties and methods. Aside from the lack of a constructor function, all the same rules apply in regards to prototypal inheritance.

Note that the `this` property is maintained within the context of the individual object.

```js
const car = {
  color: 'black',
  doors: 4,
  whatCar: function() {
    console.log(`${this.color} car with ${this.doors} doors`)
  }
}

car.whatCar(); // "black car with 4 doors"

const van = Object.assign(Object.create(car), {
  color: 'orange'
})

van.whatCar(); // "orange car with 4 doors"
console.log(van.color) // "orange"
```

## How I would answer this in an interview

First off, I would state that prototypal inheritance is not the same as class-based inheritance as each new object in JavaScript is inheriting properties and methods from its prototype, but is not an instance of the prototype as it is in class-based languages (there is a lot to unpack there, so be sure you understand that before you just say it).

Next, I would try and give a 'real world' example of inheritance. Fruit is a good one. All fruit has the following properties.

```js
const fruit = {
  taste: 'sweet',
  benefits: 'healthy',
  seeds: true
}
```

Given this common understanding of fruit, it's better to place this in a prototype object versus repeating these properties again and again in the creation of the individual fruit objects.

In the creation of the following fruit objects, we can create new objects based on the `fruit` prototype.

```js
const deliciousApple = Object.assign(Object.create(fruit), {
  color: 'yellow/green',
  shape: 'round',
  flesh: 'crunchy'
})

const navalOrange = Object.assign(Object.create(fruit), {
  color: 'orange',
  shape: 'round',
  flesh: 'soft'
})

const tomato = Object.assign(Object.create(fruit), {
  taste: 'prevailing factors of acid and sugar',
  color: 'red',
  shape: 'round',
  flesh: 'soft'
})
```

And yes ... a tomato is a fruit!
