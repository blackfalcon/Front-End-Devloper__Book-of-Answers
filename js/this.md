# Explain how this works in JavaScript

IMHO, this is a HUGE question to drop on someone in an interview. But, it is a concept that if you don't understand, you will find it very hard and very confusing to program anything in JavaScript.

Simply put, `this` is a contextual reference pertaining to the action being performed or the data being presented. The `this` keyword can be used to access values, methods and other objects that are context specific.

There are 5 ways that a `this` will get it's value

1. Within the context of a function
1. Within Methods and Objects
1. Within a Constructor
1. When a function is invoked via `.call()`, `.apply()` and `.bind()` methods
1. What about the `=>` function?

Before you try to understand any of the following, are you sure you understand what a [function](http://learningjs.anotheruiguy.com/thingsToKnow/functions.html) is? What is a [method](http://learningjs.anotheruiguy.com/thingsToKnow/methods.html) and how can you create them inside [objects](http://learningjs.anotheruiguy.com/thingsToKnow/objects.html)? What about a [constructor](http://learningjs.anotheruiguy.com/thingsToKnow/constructors.html)? Click the links if you need some background info.


## Within the context of a function

...

## Within Methods and Objects

...

## Within a Constructor

...

## Invoked via .call(), .apply() and .bind() methods

...

## What about the => function?

... I need to learn this ...

## How I would answer this in an interview

`this` is an object in JavaScript that can be populated with data based on context. The real power of `this` is that you can create single functions using the `this` keyword and based on input, event, or context, and you have a lot of flexibility as to how your function will behave.

Imagine having to write a click event, or object method, without `this`? How would you do that? How much code will it take? Hint: all answers are bad and should never be discussed out loud.
