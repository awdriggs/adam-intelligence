# Callback Function    

In javascript “callback” function is just like a placeholder, it is a function you will “call back to later”.
    
Here is a stupid but simple example…    
```js
console.log("fun");

// this is a function that returns some random way of saying hello
// we will callback to this function from another function
function randomGreeting() {
	let greetings = ["hello", "hey", "what's up", "yo", "'sup"]; //a list of possible greetings
	let greetIndex = Math.floor(Math.random() * greetings.length); //create a random index
	let greet = greetings[greetIndex]; //select the greeting at the random index
	
	return greet; //this sends the greet out at the end of the function
}

// this function takes in two parameters: 
// 1) a string for name and 
// 2) a function to callback to later
function sayHey(name, callbackFunction){
	//this line is executing the call back function to get the greeting, then combining it with a space and the name given
	let message = callbackFunction() + " " + name;  
	console.log(message); //prints the message to the console
}

//now lets use it!
sayHey("driggs", randomGreeting); //notice we're passing the function in as the second parameter, without ()
//prints "Hey driggs" or some other random greeting
```

In this example we are passing `randomGreeting` as a callback function

But why would we do this?

1. this is just an example, its not meant to be very useful
2. BUT say we wanted to have a bilingual option, then we can create another callback function for a different language.

```js
//adding a new function for spanish
function randomSaludo() {
	let greetings = ["hola", "buenas", "cómo le va", "que tal"]
	let greetIndex = Math.floor(Math.random() * greetings.length); 
	let greet = greetings[greetIndex]; 
	
	return greet; 
}

//now we can chose which callback to use without changing the sayHey function
sayHey("David", randomSaludo); //prints something like "hola David"
sayHey("Yafan", randomGreeting); //prints somehting like "'sup Yafan"
```

Now for a more complex but more useful example…an event listener for a button

- in html I have this button`<button class="action">Press Me</button>`
- in javascript I want to do something anytime that button is clicked.
- javascript has an `addEventListener` that expects a type of event as the first parameter and a callback function as the second parameter like this. `someElement.addEventListener("eventName", someCallBackFunction)`
- The callback function will run when the event is heard.

```js
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

```js
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
