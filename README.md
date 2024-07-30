# JAVASCRIPT FOR HACKERS 101

### MADE WITH  ☕ & ❤️ BY ENOCH

# Introduction

Welcome to my JavaScript notes repository! This project provides comprehensive and beginner-friendly notes on JavaScript, curated from my learning experience. As someone passionate about web and application security, I found it essential to master backend technologies, starting with JavaScript as a foundational language.

These notes are designed to help new programmers understand JavaScript concepts and prepare for more advanced topics in Node.js and Express.js. Whether you're a budding developer or an aspiring ethical hacker, these notes will guide you through the essentials of JavaScript.

## Key Features
* **Beginner-Friendly Explanations**: Clear and concise explanations of JavaScript concepts.
* **Practical Code Examples**: Real-world examples to illustrate key points.
* **Structured Learning Path**: Organize content to build your knowledge step by step.

## Prerequisites

- Good understanding of basic JavaScript syntax
- Willingness to learn
- Patience

# Objects in JavaScript

```jsx
const car = { //declaring object
    brand: "Hyundai", //properties and values
    model: "City",
    year: 2019,
};

console.log(car.brand); //accessing properties of an object
```

- **Car** is an object, with properties inside it like **brand**, **model** etc.
- Properties can hold values
- We can also have a function inside an object, remember to use function brackets after the function name

> 💡
> **A function inside an object is called a method!**


# Methods

Methods are functions that are inside an object. Similar to how we access the properties and their values inside an object. Similarly, we can access the object's methods.

```jsx
const car = { 
    brand: "Toyota", 
    model: "Innova",
    year: 2019,
		slogan: function(){ //setting a function as property in a method
				console.log("Let's Go Places")}
};

car.slogan(); //calling the slogan() method

//The slogan property is a method here because it's a function inside an object

```
```txt
OUTPUT:
Let's Go Places
```

## Constructors / Constructor Function

A constructor function is simply a function that creates **objects** for us.  We can use it to create objects in our code. It helps us to create an instance of a class (blueprint) and therefore remove
code duplication. 
We use a keyword called “**new**” which says that we need a new object


> 💡 By convention, A constructor function's first letter always starts as a capital letter



```scala
function Person(name){
	this.name = name
}

const user_1 = new Person('Enoch'); //creating a new object from the class Person
console.log(user_1); 
```

```scala
OUTPUT:

Person {name: 'Enoch'}
name: "Enoch"
[[Prototype]]: Object

//As we can see in the red highlighted output, the constructor made an object for us
```

>🤔 **But if we look closely, our function (Person) is not returning anything, how is it then assigning the object to the user_1 variable?**

When we use the new keyword when creating a new object, JavaScript automatically does two important things behind the scenes (We won’t see any of that happening)

* The first thing that JavaScript does is that it creates an empty object, and the “**this**” keyword points to the object which will store the parameter that we gave while creating a new object as properties inside the object 
* And Secondly, it returns the object that the “**this**” keyword points and stores it inside the variable which we used to assign a new instance of the class (**the variable user_1 in this case**) and when we display it out, the object which is stored inside the variable is displayed.

### Let’s look at another example to understand the concept thoroughly

```scala
function Vehicle(type){

    this.type = type;         /* When we use a "this" keyword,
                              An empty object is created and the “this” keyword points to that object. */

    this.year = 2001;        // Since there is already an object, we are adding a new property to it

    console.log(this);

}

const v1 = new Vehicle("car"); //creating a new object

```

```scala
OUTPUT:

Vehicle {type: 'car', year: 2001}
type: "car"
year: 2001
[[Prototype]]: Object
```

### Creating objects without the use of constructors

```jsx
const user_1 = {
    name: 'Enoch',
    introduce: function(){      				//creating a method
        console.log("My name is ${this.name}");
    }
}

const user_2 = {
    name: 'Benjamin',
    introduce: function(){
        console.log("My name is ${this.name}");
    }
}

const user_3 = {
    name: 'Ram',
    introduce: function(){
        console.log("My name is ${this.name}");
    }
}

console.log(user_1.name);

console.log(user_2.name);

console.log(user_3.name);

```

### Creating objects using constructors

```jsx
function Person(name){
	this.name = name
	this.introduce = () => {                              //creating a method
		return "My name is ${this.name}" 
	}
};

const user_1 = new Person('Enoch');
console.log(user_1);

const user_2 = new Person("Benjamin");
console.log(user_2);

const user_3 = new Person("Ram");
console.log(user_3);
```


>**Notice the difference between the code that uses constructors and the one
>without using constructors. Using constructors will allow us to write code without
>duplication and overall improve the readability of the code.**


## Digging deeper into the “This” keyword concept

In JavaScript, the **`this`** keyword refers to the current object or context. The value of **`this`** dynamically changes depending on the context in which it is used.


> ⚠️ **The `this` keyword when used inside a method will be limited to the method that it is in. But when the `this` keyword is used inside a  regular function, it will refer to the global object which is a window in the case of browsers and global in node.**


### Demonstrating the workings of  **`this`** keyword inside a method

### EXAMPLE 1

```jsx
const vehicle = {

	type: 'car',
	start(){
		console.log(this);
	}
};

vehicle.start();
```

```scala
OUTPUT:

{type: 'car', start: ƒ}
start: ƒ start()
type: "car"
[[Prototype]]: Object
```

Because **``start()``** is a method inside the vehicle object, the "this" keyword references the vehicle object.


### EXAMPLE 2

```jsx
const vehicle = {

	type: 'car',
	start(){
		console.log(this);
	}
};

vehicle.stop = function(){
    console.log(this);
};

vehicle.stop();
```

```scala
OUTPUT:

{type: 'car', start: ƒ, stop: ƒ}
start: ƒ start()
stop: ƒ ()
type: "car"
[[Prototype]]: Object
```

>**Even if we were to add another method to the object later on, the `this` keyword will still reference the vehicle object. 
>Because, again the stop method is inside the vehicle object**



### Demonstrating the workings of  **``this``** keyword inside a regular function

```jsx

function someRandomFunction(){
	console.log(this);
};

someRandomFunction();

```

```scala
OUTPUT:

Window {0: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
```

>**Just like we learned previously, when the "this" keyword is used in a regular function, it will refer to the window object**

### Manipulating properties in an object

```jsx
car.year = 2050; //will change the year property of the Car object

car.price = "10 lakhs"; //will add a new property called price to the Car object

delete car.price; //will delete the price property from the Car object
```

## Displaying outputs of an object

### Using Dot notation

```jsx
console.log(car); //will display all properties & values inside the Car object
console.log(car.brand); //will display the value inside the brand property
console.log(car.year); //will display the value inside the year property
```

```scala
OUTPUT:
{brand: 'hyundai', model: 'City', year: 2050}

Hyundai

2050
```

### Using Bracket Notation

There are a few instances where we need to use the bracket Notation instead of the Dot notation
For example, if we are trying to display a property called **delivery-time**, JavaScript will try to perform subtraction, 
so we need to use the **``square brackets``** and add quotes around the property

```jsx
console.log(car.delivery-time); //doing this will throw an error

console.log(car['delivery-time']);//instead we use square brackets
```

## Convert JS Objects **to JSON** and vise-versa

We can use a Build-in Object called **JSON** to convert a JavaScript object to JSON

We use a method called **`.stringify()`** to do that

We can convert a JSON to a JavaScript object using the same Build-in Object called **JSON** but by using another method called **`.parse()`**

```jsx
const jsonString = JSON.stringify(car); //converts & stores the **Car** property as JSON 
console.log(jsproperty) //displays the JS property as JSON
```

```scala
OUTPUT:
{"brand":"Hyundai","model":"City","year":2050}
```

```jsx
const jsproperty = JSON.parse(jsonString); //converts the JSON back to JS object
console.log(jsproperty) //displays the JS property
```

```scala
OUTPUT:
{brand: 'Hyundai', model: 'City', year: 2050}
```

## localStorage Object

The localStorage object in JavaScript can store data locally in a user’s browser. It can hold up to 10 MB of data. localStorage object has many methods like setItem, removeItem, and a few others.

```jsx
<h1>BUTTON FUNCTIONALITY</h1>
    
<button class="click-button">Click Me!</button>
  
localStorage.setItem('name', 'BOB') //key = name & value = BOB
  

var name = localStorage.getItem('name') //retrieving value from key 'name'

var message = () => { alert("Welcome back, " + name +'!')};
    
document.querySelector(".click-button").addEventListener('click', message);

```

The setItem and removeItem method takes two parameters. 
The first parameter is the key and the second parameter is the value that would be stored in the key.

We can use the getItem method to get values by providing a parameter which is the key of the value we need to retrieve.

## setTimeout function

The **`.setTimeout()`** is a built-in function used to time an event to occur. This function takes two parameters, the first one being the function to be executed and the second parameter is the amount of delay to be set. The time delay is set in milliseconds. Eg: 3 seconds would be 3000 ms.

```jsx
setTimeout(function(){
	alert("Timeout!")//callback function
}, 3000);

//A function that will alert “Timeout!” after 3 seconds
```

## Asynchronous Code

Asynchronous code will **not** wait for a line to finish before going to the next line and executing the code. 

```jsx
function performAsyncOperation() {
  // Simulate a long-running operation that takes 3 seconds
  setTimeout(() => {
    alert("Async operation completed!");
  }, 3000);
}

alert("Starting async operation");
performAsyncOperation();
alert("Continuing main program execution");
```

## Synchronous Code

Synchronous code **will** wait for a line to finish before going to the next line and executing the code. 

```jsx
function simulateDelayedOperation() {
  // Simulate a long-running operation with a delay
  const startTime = new Date()
  console.log("Starting delayed operation...");
  let count = 0;
  while (count < 9999990000) {
    count++;
  }

  const endTime = new Date()
  console.log('Completed executing main block' )
  totalTime = endTime - startTime
  console.log("Time taken: " + totalTime + " ms");
  
}

simulateDelayedOperation();
console.log("Hello") //will be printed after a delay of 12.6 seconds
```

## setInterval

**`.setInterval()`** is a built-in function that takes two parameters as the **`.setTimeout()`** function. 
Instead of a delay after which the function will be executed, **setInterval function repeats the function** with a delay given in the parameter between each execution of the function. For example, if we set 3000 ms, the function will run every 3 seconds.
It also takes 2 parameters. The first parameter is the function and the second parameter is the time interval in between the execution of the function.

```jsx
setInterval(function(){
	alert("Interval 1!");
}, 3000);

//This function will alert "Interval 1!" every 3 seconds
```

## forEach function

The **`.forEach()`** function is used to loop through an array and it is the preferred way to loop through an array. The **`.forEach()`** function takes a function as an input and we can set parameters to the function, The first parameter the function takes is a variable, the variable will store the items inside the array as the **`.forEach()`** function loops through it. 
The second parameter is a variable  that will store the index value of the items that the value **`.forEach()`** function loops through.
So, the first parameter which is a variable (**can be named as per our requirement**) will store the item inside the array and the second parameter which is also a variable (**can be named as per our requirement**) will store the corresponding index position of the item in the list.

```jsx
things = [                          //Array
	'todo 1',
	'todo 2',
	'todo 3',
	'todo 4',
	'todo 5'
].forEach(function(item, pos){ //item is the value & pos is the index of the value
	console.log(item);
	console.log(pos);	
});
```

```scala
OUTPUT:

todo 1
0

todo 2
1

todo 3
2

todo 4
3

todo 5
4
```

## Map function

The **`.map()`** function is a core feature of modern JavaScript and it is a powerful and commonly used function. The map function works almost similarly to the **`.forEach()`** function but with a small difference. While the **`.forEach()`** method iterates through each element in an array, the **`.map()`**function also iterates through each element in the array, But it returns with an Array of values it iterated through the original array. To achieve this, the **`.map()`** function takes an argument and uses it as a temporary variable to store the values in the array the **`.map()`** function iterates through so they can be returned. It’s also important to note that  **`.map()`** function **DOES NOT** modify the original array. Unlike **`.forEach()`**, which can modify the elements within the original array, the **`.map()`** function only creates a new array with transformed values and leaves the original array untouched.

```jsx
const numbers = [2,4,6,8,10] //original array

const doubleNumbers = numbers.map(individualNumbers =>{
  return individualNumbers * 2
})

console.log(doubleNumbers)

```
>**This code will return an array with the values in the "numbers" array multiplied by 2.
>Notice the highlighted variable, it's the temporary variable that will store the values that are iterated through the original array,
>temporarily. It can be named anything but it's often named an item or element**


### We can write the above code in a much cleaner way using the ES6 syntax**

```jsx
const numbers = [2,4,6,8,10]

const doubleNumbers = numbers.map(e => e * 2)

console.log(doubleNumbers)

```
>**Remember, in ES6 syntax, if we are only returning a single item, we don't
>need to put it in curly brackets. This way of writing JavaScript code is
>more cleaner and readable**


## Find method

The **`find()`** method is used to get the value of the first element in an array that satisfies the provided condition. It takes in a function as a callback function, So we need to create a function to search for the element we want and return it, and pass this function to the **`find()`** method as the callback function. Let’s understand this with a code example:

```jsx
const people = [    //An array with 3 objects
  {
    name: "Enoch",
    age: 22,
    employed: true
  },
  {
    name: "Annie",
    age:34,
    employed: true

  },
  {
    name: "Ram",
    age: 18,
    employed: false
  }
]

function search(people){
  return people.name === "Ram"
  }

/*This function takes in the names array as an argument and returns the entire
  object if the object's name value matches with the value we provided */

console.log(names.find(search)) 

//Displaying the output of the find function which takes in the search function as an argument which we defined above.

```
```scala
OUTPUT:

{ name: 'Ram', age: 18, employed: false }

```

### We can take this a step further and access just the individual values instead of the entire object itself

```jsx
console.log(names.find(search).age) //Displays the age value from the object
console.log(names.find(search).employed) // Displays a boolean value
```

```scala
OUTPUT:

18
false
```

## Filter Method

The **`filter()`** method is a very commonly used method in JavaScript. This method allows us to filter out elements in an array or an object. This allows us to be provided with data that is relevant and ignore the rest of them. The **`filter()`** takes in 3 parameters, But we commonly use it with a callback function that does the process of filtering out things. 
Let’s understand it with a code example:

```jsx
const array = [2,4,-1,45,-3,0,-1,9,12]

const filtered = array.filter((e)=>{
    return e >= 0;
})

console.log(filtered);
```
```scala

OUTPUT:

[ 2, 4, 45, 0, 9, 12 ]
```

>**We define an array named `array` containing both positive and negative numbers
>A constant variable called `filterer` stores the results of the `array.filter()`
>method, which filters the "**array**" for elements greater than or equal to zero.
>The `array.filter()` method iterates through the array using the temporary 
>variable `e` and returns values where `e` meets the condition. 
>Finally, the variable `filtered` containing the filtered results is displayed.**

## Arrow Functions

The arrow function in JavaScript mostly works the same way as a regular function. 
Arrow functions **DO** **NOT** support hoisting!

```jsx
const regularFunction = function(param1, param2){
	console.log("Regular Function!");
};

const arrowFunction = (param1, param2) =>{
	console.log("Arrow Function!");
};

arrowFunction();
regularFunction();

```
```scala
OUTPUT:

Arrow Function!
Regular Function!
```

## One Parameter arrow function

For Functions with one parameter, the function brackets covering the parameter(s) are optional

```jsx
const oneParam = param => { //no function brackets for the parameter
	console.log(param + 1)
};

oneParam(2);

const function = (param) => { //with function brackets for the parameter
	console.log(param + 1)
};

oneParam(2);
```

```scala
OUTPUT:

3
```

## **One Line function**

When an arrow function has only one line in it, we can put it in the same line as the arrow, and the curly brackets are optional, and to also remove the return keyword if we are returning anything

```jsx
const oneLine = () => 2 + 3; //one line function with return
console.log(oneLine());

const function = () => { //same function as above but without the shortcuts
	return 2+3;
};

```
```scala
OUTPUT:

3
```

## Query Selectors

### querySelector

The **`.querySelector()`** method can be used to target HTML elements, It returns **only** the first element within the document that matches the specified selector, or group of selectors. 
If no matches are found, **null** is returned.

```jsx
<button class="click-button">Click Me!</button> //HTML code to create the button

const button = document.querySelector('.click-button'); //storing it to a variable
```

### querySelectorAll

Because the **`.querySelector()`** method only returns the first HTML element with the specified class name, we use the **`.querySelectorAll()`** method will return a list of **ALL** HTML elements that match the specified class name. It will be in an array format. We can use array indexing to target individual elements from the list of elements returned to use by the **`.querySelectorAll()`** method.

```jsx
<button class="click-button">Click Me!</button>
    <button class="click-button">Don't Click Me!</button>
    <button class="click-button">Please Click Me!</button>
    <button class="click-button">Please don't Click Me!</button>

    var queryselector = document.querySelector(".click-button");
    console.log(queryselector);

```
```scala
OUTPUT:
```
```jsx
<button class="click-button">Click Me!</button>

//notice the difference between both the methods**

var queryselectorall = document.querySelectorAll(".click-button");
    console.log(queryselectorall);
```
```scala
OUTPUT:

NodeList(4) [button.click-button, button.click-button, button.click-button, button.click-button]
    
```

## Event Listener

Event Listeners are used to listen to an event and perform certain functions when the event occurs
An event listener commonly takes two parameters, The first one is the event or trigger and the second parameter is the function to be executed in the event.

### addEventListener

This method is used to add an event listener to an HTML element


>💡 **We can add multiple event listeners to an element**



```jsx
<button class="click-button">Click Me!</button> 

		const button = document.querySelector('.click-button'); 
		button.addEventListener('click', () => { 
		alert('I was clicked!');
  });

//We used an arrow function to give the alert
```

We can also store the function to be executed in the occurrence of an event, to a variable and use it instead of writing a function in the second parameter of the event listener. 
Example code below: 

```jsx
<button class="click-button">Click Me!</button>
 
   const button = document.querySelector('.click-button');

	 const event = () => { alert("I was clicked!")}; //storing funtion to a variable
   
button.addEventListener('click', eventListener); //using the variable 
```

### removeEventListener

This method is used to remove an event listener from an HTML element

```jsx
<button class="click-button">Click Me!</button>

        const button = document.querySelector('.click-button');
        const event = () => { alert("I was clicked!")};
        button.addEventListener('click', eventListener);//adding

        button.removeEventListener('click', eventListener);//removing

/* We had to store the alert function to a variable (eventListener) 
to remove it later using the removeEventListener method */
```

### addEventListener with ‘keydown’ event

If we want to listen to the keyboard inputs, we must use the keydown event listener.

```jsx
document.body.addEventListener("keydown", (event) =>{
            alert(event.key + " was pressed");
        });
```
>**We are adding an event listener to the body, the event listener method takes three parameters in this case.
>The first parameter is the event to listen to.
>The second parameter in brackets (event) will store the event into it.
>The third parameter is the function to be executed when the event occurs

>The event.key in the alert function will output the key pressed.
>The `.key` method is used to access the data that reveals which key was pressed on the keyboard**



### Event Listener which only runs once

We might sometimes want to listen to an event only once, and after that, we do not need the event listener to function anymore. To perform that, we can give it  a third parameter to the **`.eventListener()`** method.

```jsx
<button style="margin: 30% 50%;" id="button">CLICK ME</button>
  
const button = document.querySelector("#button");
button.addEventListener("click", ()=>{alert("Button was clicked")}, {once: true});

//The event listener will only listen for once and after that, it will stop.
```

## Event Listener Bubbling concept (Event bubbling)

The event bubbling, or the bubbling concept in event listener is a concept which involves the process of the control going from the closest element to the farthest element. For example, let’s say we have a div called **`div1`**, a div inside it called **`div2`** and another div inside it called **`div3`**. Now if we were to add event listeners to all of the **divs** with a callback that alerts some message, A click event on **`div3`** triggers the event listener attached to **`div3`**. The event then "**Bubbles up**" to **`div2`**, and its event listener is invoked if there is one. Finally, the event continues to bubble up to **`div1`**, and its event listener is invoked if one is attached.  So this results in all the event listeners of the divs being triggered. This concept is called Event Bubbling or Bubbling.

### Example to demonstrate the bubbling concept

```jsx
<body>
    <div class="grandparent">
        <div class="parent">
            <div class="child"></div>
        </div>
    </div>
<body>
```

```css

  .grandparent{
        position: absolute;
        height: 300px;
        top: 5%;
        left: 25%;
        right: 25%;
        height: 60%;
        background-color: red;
    }
    .parent{
        position: relative;
        height: 100px;
        top: 20%;
        margin-left: 20%;
        margin-right: 20%;
        height: 60%;
        background-color: blue;
    }
    .child{
        position: relative;
        height: 50px;
        top: 30%;
        margin-left: 20%;
        margin-right: 15%;
        height: 50%;
        background-color: green;
    }
```

```jsx

    const grandparent = document.querySelector(".grandparent");
    const parent = document.querySelector(".parent");
    const child = document.querySelector(".child");

    grandparent.addEventListener("click", () => alert("Grandparent 1"));
    parent.addEventListener("click", () => alert("Parent 1"));
    child.addEventListener("click", () => alert("Child 1"));
    document.addEventListener("click", () => {alert("Document 1")});
   
//the control goes from innermost DIV to the outermost
```

## Event Listener Capturing concept (Event Capturing)

The event bubbling or the bubbling concept in event listener is a concept in which during the capture phase, the event starts from the outermost ancestor (element with true capture set) and goes towards the target element. The capturing element's event listener is executed before the event reaches the target element. After the capturing elements have processed the event, the event continues with the target element. Then, the event bubbles up from the target element to the outermost ancestor.

### Example to demonstrate the capturing concept

```html
<body>
    <div class="grandparent">
        <div class="parent">
            <div class="child"></div>
        </div>
    </div>
<body>
```

```css

    .grandparent{
        position: absolute;
        height: 300px;
        top: 5%;
        left: 25%;
        right: 25%;
        height: 60%;
        background-color: red;
    }
    .parent{
        position: relative;
        height: 100px;
        top: 20%;
        margin-left: 20%;
        margin-right: 20%;
        height: 60%;
        background-color: blue;
    }
    .child{
        position: relative;
        height: 50px;
        top: 30%;
        margin-left: 20%;
        margin-right: 15%;
        height: 50%;
        background-color: green;
    }

```

```jsx
const grandparent = document.querySelector(".grandparent");
const parent = document.querySelector(".parent");
const child = document.querySelector(".child");

grandparent.addEventListener("click", () => alert("Grandparent 1"),{capture: true});
parent.addEventListener("click", () => alert("Parent 1"));
child.addEventListener("click", () => alert("Child 1"));
document.addEventListener("click", () => {alert("Document 1")});
```

>**The control goes to the grandparent DIV because we have set capture as true 
>for the grandparent DIV, after that the control goes back to the clicked div**


## Event Delegation

Sometimes we might select all html elements we want using the **`.querySelectorAll()`** method and later on we decided to create one more such element. But interestingly, the new element will not be selected by the **`.querySelectorAll()`** method. That’s because we created the HTML element after we have used the query selector. Although we can explicitly write code for the new element it is a good practice to include it in one go. So to solve this problem, we use Event Delegation.
Suppose we want to event listen for click on the HTML elements, we can add an event listener to the document’s body and check if the click was performed on the elements that we wanted and perform functions based upon it. We can let the functions be performed if the click was on our desired elements or otherwise simply ignore the clicks.

### THE PROBLEM

```jsx
                            

const divs = document.querySelectorAll("div"); //selecting all the DIVs
    divs.forEach(div => {
        div.addEventListener("click", () => {console.log("Hi")});
    });

    const newDiv = document.createElement("div"); //creating a new DIV

    newDiv.style.position = "relative"
    newDiv.style.marginLeft = "75%"
    newDiv.style.top = "37px"
    newDiv.style.width = "200px"
    newDiv.style.height = "545px"
    newDiv.style.backgroundColor = "purple"

    document.body.append(newDiv) //appending the new DIV to the document
```

>**In the above code, we have selected all the div elements using the
>`.querySelectorAll()` method, but later on we can see that we have created a new
>div element using the `.createElement()` method. Since we have already selected
>all the divs before itself, the newly created DIV will not be included in it.
>The Event Delegation concept solves this problem.**

	
### THE SOLUTION

```jsx
const divs = document.querySelectorAll("div");

//performing checks to verify if the mouse clicks were on the DIV element
			
    document.addEventListener("click", e => { 	
        if(e.target.matches("div")){
            alert("Hi");
        }
    })
  
    const newDiv = document.createElement("div");

    newDiv.style.position = "relative"
    newDiv.style.marginLeft = "75%"
    newDiv.style.top = "37px"
    newDiv.style.width = "200px"
    newDiv.style.height = "545px"
    newDiv.style.backgroundColor = "purple"

    document.body.append(newDiv)
```
>**In the above code, we have written a check to verify if the mouse clicks by
>the user were on the DIV elements or not. We are using a method to do this.
>If the clicks matches the condition, The alert function will be executed or else
>the clicks will be ignored. This is a useful real-life application of 
>the Event Delegation concept.**


## Useful DOM Manipulation techniques

### Append

The **`.append()`** method is used to append any HTML elements and strings. We can provide an append method with multiple parameters which can be used to append many things at once.

```jsx
document.body.append("Hello");//single parameter

document.body.append("Hello ", "What is your name?");//multiple parameter
```

### Create Element

The **`.createElement()`** method can be used for creating or adding an HTML element. We can add a **‘DIV’** element for example. 

```jsx
var div = document.createElement('div'); //creating a div element
document.body.append(div); //adding/appending the div to the pagearray
```


>⚠️ **Creating an element to be added to the document using JavaScript is not enough, we must also add it. For this reason we use the append method to append the element >to the document’s body.**


### Inner Text

The **`.innerText()`**   method is used for adding texts into an HTML element. Suppose we want to add a text inside the div we created using the **`.createElement()`** method, we can simply use the **`.innerText()`**method to do that

```jsx
var div = document.createElement('div');
document.body.append(div);
div.innerText="Hello" //adding text to the div
```

### Text Content

The **`.textContent()`** method works similar to the **`.innerText()`** method. When adding text, there is no difference in how both methods work. The difference is that the **`.innerText()`** method checks to see if the text is set to be hidden by the CSS or if it is visible. If it’s hidden, then the specific text won’t be made visible by the **`.innerText()`** method whereas the **`.textContent()`** method will display an element no matter if it is set to be hidden by the CSS. 


>⚠️ **The `.textContent()` method will also display the exact text content. It will display all the spacing as well as the indentations in the HTML code**



### Inner HTML

The **`.innerHTML()`** method is used to add HTML elements to the body. It can also be used to add HTML code inside another HTML element

```jsx
document.body.innerHTML="<h4>INNER HTML</h4>" 		//adding HTML to the body

div.innerHTML="<h1>HELLO</h1>" //adding html code inside another the div element
```

### Remove

We can remove content from our HTML by using the **`.remove()`** method.

```jsx
<h1 class="greet">Hello</h1>
var hello = document.querySelector(".greet");

hello.remove(); //removing the html element with class "greet"
															
```
### OR

```jsx
document.querySelector(".greet").remove(); //or we can just remove it directly
```

## Essential DOM Manipulation Techniques

### Get Attribute

The **`.getAttribute()`**e method is used to display the attributes of an HTML element. Attributes like class, title, id, etc can be displayed using the **`.getAttribute()`** method. This method takes one parameter that is the attribute type of an HTML element we want to display. 

```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
</body>
```
```jsx
alert(document.querySelector(".how").getAttribute("title"));
```

>**The querySelector method will select the HTML element with class ".how" and it
>will display the tile that has been set to it.
>The output will be an alert pop-up with the text "alright?"**

### Set Attribute

The **`.setAttribute()`** method is used to set attributes to an HTML element. Attributes like class, id, title, etc can be set to an HTML element by using the **`.setAttribute()`** method. This method takes **two** parameters. The first parameter is the attribute which we want to set, and the second parameter is the value that we want to set to the attribute.


>💡 **We can provide the parameter with an attribute which does not exist in the html element 
> and it will create the attribute and set the value we give.**



```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
</body>
```

```jsx
document.querySelector(".water").setAttribute("id", "under" );
```

>**This will select the HTML element with the class ".water" and will create an**
>`ID` **attribute and set its value to "under"**

```jsx
alert(document.querySelector(".water").getAttribute("id"));
//The output will be an alert box with the text "under"
```

### Remove Attribute

The `.**removeAttribute()**` method will remove an attribute from an HTML element provided that the attribute exists in the first place. Attributes like class, id, title, etc can be removed
This method takes one parameter which is the name of the attribute which we want to remove.

```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
</body>
```

```jsx
document.querySelector(".how").removeAttribute("title");
//removing the title attribute

alert(document.querySelector(".how").getAttribute("title"));
```
```scala
OUTPUT: 

An alert box with the text "NULL"
```

## Class List

The Class List contains methods that let us manipulate classes in HTML elements.

### Class List Add

The **`.classList.add()`** method lets us add classes to an HTML element. It takes one input that's the name of the class we want to add to the HTML element.

```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3>Please help me</h3>
</body>
```

```jsx
document.querySelector("h3").classList.add("send-help"); //adding class

alert(document.querySelector("h3").getAttribute("class"));//displaying the class
```
```scala
OUTPUT:

An alert box with the text "send-help"** 
```

### Class List Remove

The **`.classList.remove()`** method is used to remove a class from an HTML element. This method takes one input and it is the name of the class that we want to remove from the HTML element.

```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="send-help">Please help me</h3>
</body>
```

```jsx
//removing the class
document.querySelector(".send-help").classList.remove("send-help");

alert(document.querySelector("h3").getAttribute("class")); //displaying classes
```
```scala
OUTPUT:

A blank alert box
```

### Class List Toggle

The **`.toggle()`** method when used either add the class to the HTML if it doesn’t exist or it removes the class if it exists in the HTML element. This method takes two parameters. The first parameter is the class name we want to toggle and the second parameter is a boolean value.


>📌**If the boolean value is set to “**true**” then it will add the class which we provided to the HTML element and if we set the value to “**false**” then >it will remove the class from the HTML element.**

```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="send-help">Please help me</h3>
</body>
```
```jsx
document.querySelector("h3").classList.toggle("send-help"); //toggling
```

```scala
OUTPUT:

false 

//the class "send-help" exists so it was removed
```
```html
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="">Please help me</h3>
</body>
```
```jsx
document.querySelector("h3").classList.toggle("send-help"); //toggling
```
```scala
OUTPUT:

true //the class "send-help" doesn't exist so it was added
```

## Style

The style property contains can be used to manipulate the CSS of an HTML, directly using JavaScript. The style property is a property to access the CSS properties of any HTML element

### Style Color

The **`.style.color`** property can be used to change the colour of a text in an HTML element.

```html

//Defult HTML Code

<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="send-help">Please help me</h3>
</body>
```html
```
```jsx

document.querySelector(".send-help").style.color = "red"; //setting color to red
```

```html

//HTML Code after manipulation. Notice the highlighted code below
<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="send-help" **style="color: red;**">Please help me</h3>
</body>
```

### Style Background Color

The **`.style.backgroundColor`** property lets us change the background color of an HTML element.
It works in the same way as the **`.style.color`** property.

```html

//Defult HTML Code

<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="send-help">Please help me</h3>
</body>
```
```jsx

//setting the background color to red
document.querySelector(".send-help").style.backgroundColor="red";
```

```html

//HTML Code after manipulation. Notice the highlighted code below.

<body>
    <h1 class="greet">Hello</h1>
    <h2 class="how" title="alright?">How are you?</h2>
    <h2 class="water">I am under the water</h2>
    <h3 class="send-help" style="background-color: red;">Please help me</h3>
</body>
```

# JavaScript Promises

Promises in JavaScript are a way of assuring that a function will do something. We have two cases in promises, the first one is the resolve case which essentially means that the code has completed or resolved the promise that was made, and the second one is the reject case which means that the has not been able to complete or resolves the promise it has made. The function returns something in both cases whether it resolves or rejects the promise. This way we can write asynchronous code that is non-blocking and the code runs smoothly. Promises are a way to handle asynchronous code in JavaScript. They allow you to write code that will be executed when the asynchronous operation is complete, and they also allow you to handle errors that may occur.

```jsx
function car(){

   return new Promise(function(resolve,reject){
       //resolve("Toyota")
       reject("Hero")
   })
}

const vehicle = car();
vehicle.then(function(onSuccess){
    console.log(onSuccess + " is a valid car name!")
}, function(onError){
    console.log(onError + " is not a valid car name!")
})
```
>**After we have made a promise, we have to call multiple methods on it. We
>have used the **then()** method that is used to describe what to do when the
>the promise returns the data. So we have written a function with a parameter called
>onSuccess** **which references to the return data of the Promise object.
>And in the case of a reject, we have created another function with a parameter
>called onError which is also a reference to the return data of the Promise
>object.**


## Phases in a Promise

There are 3 phases in a promise. 

### PENDING

This is the initial state of a promise. It means that the asynchronous operation has not yet started or finished.

```jsx
let check = new Promise((resolve,reject) =>{
    let sum = 1+1;   
})

check.then((message) =>{
    console.log("Correct Calculation!")
}).catch((message) => {
    console.log("Wrong Calculation!")
})
```

```scala
OUTPUT:

'Promise {<pending>}'**
```
>**In this code, We have used the promise object but we haven't set any rules
>for the `resolve` and reject phase. So by default, the code is pending**

### FULFILLED

This means that the asynchronous operation has been completed successfully.

```jsx
let check = new Promise((resolve,reject) =>{
    let sum = 1+1;
    if(sum == 2){
        resolve("1 + 1 = 2");
    }else{
        reject("1 + 1 != 3");
    }
})

check.then((message) =>{
    console.log("Correct Calculation!")
}).catch((message) => {
    console.log("Wrong Calculation!")
})

```

```scala
OUTPUT:

Correct Calculation!
'Promise {<fulfilled>: undefined}'
```
In this code, the promise has been fulfilled, and the **resolve** case
has worked as intended because **1 + 1 = 2**


### REJECTED

This means that the asynchronous operation has failed.

```jsx
let check = new Promise((resolve,reject) =>{
    let sum = 1+1;
    if(**sum == 3**){
        resolve("1 + 1 = 2");
    }else{
        reject("1 + 1 != 3");
    }
})

check.then((message) =>{
    console.log("Correct Calculation!")
}).catch((message) => {
    console.log("Wrong Calculation!")
})
```

```scala
OUTPUT:

Wrong Calculation!**
'Promise {<fulfilled>: undefined}'
```

>**Interestingly, the log shows that the promise has been fulfilled even though
>the rejected case was executed. Why did that happen?
>If we think about it, the **catch** method has caught the rejected case successfully
>and displayed the messages successfully, so that is why the promise has been
>shown as fulfilled**

# Async/Await in JavaScript

## The problem with Promises

1. **Callback Hell (Pyramid of Doom):** Promises chaining with **`.then()`** can lead to nested structures that are hard to read and maintain, often referred to as "callback hell."

3. **Error Handling Complexity:** Handling errors in promise chains requires the use of **`.catch()`**, and errors can jump to the nearest catch block, making error handling less intuitive than **`async/await`** with **`try/catch`**.

5. **Readability Concerns:** Promise chains may be challenging to read, especially for developers new to asynchronous programming, while **`async/await`** syntax offers a more concise and readable alternative.

## The solution

On the other hand, when you use **`async/await`**, it allows you to write asynchronous code in a more synchronous-looking manner. When you mark a function as **`async`** and use the **`await`** keyword inside that function, the JavaScript engine will pause the execution of that function until the awaited promise is resolved. This makes it easier to write and understand asynchronous code.

## USING PROMISES

```jsx

function getData(){
    return new Promise((resolve,reject) =>{
        let sum = 1 + 1;
        if(sum == 2){
            resolve("Success")
        }else{
            reject("Error")
        }
    })
}

const result = getData()

result.then((data) => {
    console.log(data)
}).catch((data) => {
    console.log(data)
})

```
## USING ASYNC/AWAIT

```jsx

function getData(){
    return new Promise((resolve,reject) =>{
        let sum = 1 + 1;
        if(sum == 2){
            resolve("Success")
        }else{
            reject("Error")
        }
    })
}

async function theAsyncWay(){
    try{
        let result = await getData()
        console.log(result)
    }
    catch (error){
        console.log(error)
    }
}

theAsyncWay()
```

> **Notice the improvement in the readability of the code written using** **`ASYNC/AWAIT`**
