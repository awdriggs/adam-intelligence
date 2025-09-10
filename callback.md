# Callback Function

In javascript a “callback” is a function you will “call back to later”. Its like you are setting up a function to use from another function later on.

## A callback calculator 
Here is a stupid but simple example…
```javascript
// a function that simple addes two numbers togethert
function add(num1, num2) {
  return num1 + num2; //simple add two numbers and return them
}

// a calculate funciton with three parameters
// - a number
// - a second number
// - an operation function, this is our 'callback'
function calculate(num1, num2, operation){
  return operation(num1, num2);
}

// lets use it!

let result = calculate(4, 6, add); // do some calculation

console.log(result); // prints 10 to the console.
```

In this example we are passing `add` as a parameter in another function. Here `add` is know as a callback function.

`calculate` is holding on to `add` and will call back to it when it is called.

## Why?

But why would we do this?

1. This is just an example, its not meant to be very useful
2. BUT say we wanted to have another operation, then we can create another call back function for a different math .

```javascript
//adding a subtraction function
function sub(num1, num2) {
  return num1 - num2;
}

//without making anychanges to calculate we can use our new functionality!

result = calculate(11, 9, sub);
console.log(result); // prints 2 to the consoel.
```

### A More Useful Example

Now for a more complex but more useful example; an event listener for a button

- In html I have this button`<button class="action">Press Me</button>`
- In javascript I want to do something anytime that button is clicked.
- Javascript has an `addEventListener` function that expects a type of event as the first parameter and a callback function as the second parameter like this. `someElement.addEventListener("eventName", someCallBackFunction)`
- The callback function will run when the event is heard.

```javascript 
//my callback, super simple
function yo() {
  console.log("a button was pressed");
  //and in reality i'd do other stuff
}

//grab the button element from the dom
let actionButton = document.querySelector('.action');

//add an event listener for a button
// - click is the event i'm listening
// - yo is the callback i'm using when the event is "heard"
actionButton.addEventListener("click", yo);
```

In that example I’m using the function `yo` as my callback. Since the function has a name it is called a named function.

A very common pattern is the pass a anonymous function as a callback function. Anonymous functions are just functions without names, so they are anonymous, meaning there is no way of access them through a variable name.

This example does exactly the same thing.

```javascript
//grab the button element from the dom
let actionButton = document.querySelector('.action');

//add an event listener to that button
// - click is the event
// - anonymous callback function
actionButton.addEventListener("click", ()=>{
  //i'm inside the callback function here!
  console.log("hello from callback function");
  //and other stuff that should happen with a button click.
});
```

Hope that clears things up.

## Nerding Out
In javascript, function are known as "first class objects." This is a fancy way of saying "functions are treated like any other thing in javascript; numbers, strings, objects. So functions can be used as the parameters for other functions." 

Most modern languages treat functions this way, but older programming languages didn't.
