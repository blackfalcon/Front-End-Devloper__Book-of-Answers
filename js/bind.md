# Explain Function.prototype.bind

Using the `.bind()` function, we are able to bind data objects to a function at will. This is a big deal as this can drastically change the outcome of the function you are working with.

In the following example I will create a new object for `doorbell` that will contain its sound and a method to log that sound to the console.

```js
const doorbell = {
  sound: 'ring',
  logSound: function() {
    console.log(this.sound);
  }
}
```

By calling that object with it's method we will get the sound logged to the console. This works because the `logSound()` method has direct context to the object's `sound` attribute.

```js
doorbell.logSound(); // `ring`
```

In JavaScript we can assign a function as the value of a variable. Listen to what I am saying here, we can assign a function as the value of a variable, not just the output of the function. This makes a YUUGE difference.

For example, if we were to create a new variable, `doorbellSound` and assign the function so that it returns its value, we will get `ring`, as this is the return of the function and is assigned to the variable, not the function itself.

```js
let doorbellSound = doorbell.sound();

doorbellSound; // `ring`
```

But what if we only assign the function to the variable so that we can run that variable as a function?

```js
let doorbellSound = doorbell.sound;

doorbellSound(); // undefined
```

This doesn't work!? Why? The reason really is, when we are running the method function within the context of `doorbellSound()`, `this` is totally lost. I mean, it's just floating out in space. Think about it, when we are calling `doorbellSound()` we are calling an object method without context. So, how can we fix this? Well, this is where the `.bind()` function comes in.

At this point we know that when we assign an object's method to a variable and run that variable, we have lost context with the data we are looking for. So imagine that you can just reach out and grab some data context and shove it right back in? Well, you don't have to imagine as we can actually do this.

In the next example I am redefining the `doorbellSound` variable to `.bind()` the `doorbell` data to this context.

```js
let doorbellSound = doorbell.logSound.bind(doorbell);

doorbellSound(); // `ring`
```

## But why ... ?

Ok, so this all makes sense within this example, but why would I want to use this like this versus just accessing the object and its method directly? Well, that's a tough question to answer, so let's imagine a new scenario. Let's imagine that we have two objects. One for `doorbell` and one for `oldCar`. In each object we have a value for the `sound` that this object makes.

```js
const doorbell = {
  sound: 'ring'
}

const oldCar = {
  sound: 'AOOOGAH!!'
}
```

Then, to abstract things, let's create another object that contains the method that we can use to log the sound.

```js
const thing = {
  logSound: function() {
    console.log(this.sound);
  }
}
```

Ok, so now we have three objects, two that are specific and one that is abstract and contains the method. Can you see what's happening next? It's at this time we can create a new variable that will reference the `thing` object that has the method of `logSound` and then `.bind()` the data for `oldCar`. Holy crap ...

```js
let newThing = thing.logSound.bind(oldCar);

newThing(); // "AOOOGAH!!"
```

And what about `doorbell`?

```js
let newThing = thing.logSound.bind(oldCar);
let anotherNewThing = thing.logSound.bind(doorbell);

newThing(); // "AOOOGAH!!"
anotherNewThing(); // "ring"
```

And there you have it. If you were able to get your head wrapped around this, then give yourself a High Five! This is a tough one and its uses are vast and interesting.

## How I would answer this in an interview

Well, there is the long answer above, but that is a really long answer. The short answer is the `bind()` method, when applied, creates a new function and has its `this` keyword set to the provided value.
