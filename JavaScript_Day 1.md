# JavaScript First Steps

A practical learning guide to JavaScript fundamentals, combining the original JavaScript First Steps README with the Day 2 learning guide.

This README starts with the basics of JavaScript and gradually moves into the DOM, values and data types, operators, expressions, variables, arrays, objects, functions, methods, small projects, asynchronous JavaScript, APIs, promises, `fetch()`, `await`, destructuring, and URL processing.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Course Overview](#course-overview)
3. [What is JavaScript?](#what-is-javascript)
4. [Where to Write JavaScript](#where-to-write-javascript)
5. [DOM: Document Object Model](#dom-document-object-model)
6. [Values and Data Types](#values-and-data-types)
7. [Operators](#operators)
8. [Expressions and Variables](#expressions-and-variables)
9. [Arrays](#arrays)
10. [Objects](#objects)
11. [Functions](#functions)
12. [Quiz Project](#quiz-project)
13. [Tic Tac Toe](#tic-tac-toe)
14. [Day 2: DOM, Objects, Functions, APIs, and Async JavaScript](#day-2-dom-objects-functions-apis-and-async-javascript)
15. [Quick Reference](#quick-reference)
16. [Common Beginner Mistakes](#common-beginner-mistakes)
17. [Practice Checklist](#practice-checklist)

---

## Introduction

JavaScript is one of the main technologies used to build interactive websites.

HTML provides the structure of a page, CSS controls its appearance, and JavaScript adds behavior and interactivity.

This guide assumes basic knowledge of HTML and CSS. No previous JavaScript experience is required.

By the end of this guide, you should understand how to:

- Run JavaScript in a browser.
- Use the browser console.
- Select HTML elements with JavaScript.
- Read and change page content.
- Work with strings, numbers, booleans, `undefined`, and `null`.
- Use arithmetic and comparison operators.
- Declare and use variables.
- Understand expressions and statements.
- Work with arrays and array methods.
- Understand references and mutability.
- Create and modify objects.
- Use object methods and `this`.
- Work with nested objects.
- Create and call functions.
- Understand parameters and arguments.
- Connect JavaScript logic to the DOM.
- Build a small interactive quiz.
- Understand how arrays, objects, functions, and the DOM work together.
- Use timers, promises, `fetch()`, `await`, and destructuring.
- Read data from an API and update the page with the result.

---

## Course Overview

```text
JavaScript Basics
      ↓
DOM
      ↓
Values & Data Types
      ↓
Operators
      ↓
Expressions & Variables
      ↓
Arrays
      ↓
Objects
      ↓
Functions
      ↓
DOM + Logic
      ↓
Quiz Project
      ↓
Tic Tac Toe
      ↓
Timers, APIs, Promises, and Async JavaScript
```

The goal is not only to memorize syntax, but to understand how JavaScript represents data and how that data can control a web page.

---

## What is JavaScript?

JavaScript is a high-level, dynamically typed programming language.

It is widely used in web browsers to make pages interactive.

JavaScript can:

- Read HTML elements.
- Change text and styles.
- React to user actions.
- Store and process data.
- Perform calculations.
- Work with arrays and objects.
- Create reusable functions.
- Communicate with other systems.
- Run outside the browser through environments such as Node.js.

JavaScript is standardized as ECMAScript. The language was created in 1995 by Brendan Eich.

### First JavaScript Statement

```js
console.log("Hello, JavaScript!");
```

`console.log()` prints a value or message to the browser console.

---

## Where to Write JavaScript

There are three common ways to run JavaScript.

### 1. Browser DevTools Console

The console is useful for quick experiments.

```text
Right-click -> Inspect -> Console
```

Then try:

```js
console.log("Hello!");
```

### 2. Inline JavaScript

JavaScript can be written directly inside an HTML `<script>` element.

```html
<script>
  console.log("Hello from inline JavaScript");
</script>
```

### 3. External JavaScript File

A JavaScript file can be connected to an HTML page.

```html
<script src="app.js"></script>
```

Then `app.js` can contain:

```js
console.log("Hello from app.js");
```

Recommended structure:

```text
project/
├── index.html
├── style.css
└── app.js
```

Keeping HTML, CSS, and JavaScript separated makes projects easier to organize and maintain.

---

## DOM: Document Object Model

The Document Object Model, or DOM, is the browser's representation of an HTML document.

The browser turns HTML elements into objects/nodes that JavaScript can access and manipulate.

```text
document
└── html
    ├── head
    └── body
        ├── h1
        └── p
```

JavaScript can use the DOM to:

- Find elements.
- Read their content.
- Change their content.
- Change styles.
- Add or remove classes.
- Respond to user events.

### Selecting Elements

#### `querySelector()`

Selects the first element that matches a CSS selector.

```js
const title = document.querySelector("h1");
```

It can also use IDs and classes:

```js
document.querySelector("#title");
document.querySelector(".card");
```

#### `querySelectorAll()`

Selects all elements that match a CSS selector.

```js
const paragraphs = document.querySelectorAll("p");
```

The result is a `NodeList`.

#### `getElementById()`

Selects an element using its ID.

```js
const title = document.getElementById("title");
```

The ID is passed without `#`.

```js
document.getElementById("title"); // correct
document.querySelector("#title"); // correct with querySelector
```

#### `getElementsByTagName()`

Selects elements by tag name.

```js
const items = document.getElementsByTagName("li");
```

#### `getElementsByClassName()`

Selects elements by class name.

```js
const cards = document.getElementsByClassName("card");
```

### Selection Comparison

| Method | Purpose |
| --- | --- |
| `getElementById()` | Select one element by ID |
| `getElementsByTagName()` | Select elements by tag name |
| `getElementsByClassName()` | Select elements by class name |
| `querySelector()` | Select the first CSS selector match |
| `querySelectorAll()` | Select all CSS selector matches |

### `.length` with DOM Collections

`.length` gives the number of items in a collection.

```js
const items = document.querySelectorAll("li");
console.log(items.length);
```

The same idea works with class selections:

```js
const buttons = document.getElementsByClassName("choice");
console.log(buttons.length);
```

### `.textContent`

`.textContent` reads or changes the text inside an element.

Read text:

```js
const title = document.querySelector("h1");
console.log(title.textContent);
```

Change text:

```js
title.textContent = "New Title";
```

It is a property, not a function:

```js
title.textContent = "New text"; // correct
title.textContent();            // incorrect
```

### Changing a Web Page

JavaScript can modify an element after selecting it.

```js
const title = document.querySelector("h1");

title.textContent = "New Title";
title.style.color = "blue";
title.classList.add("highlight");
```

### DOM Refresh Behavior

DOM changes made by JavaScript normally affect the current page in memory.

```js
document.body.style.backgroundColor = "black";
```

If the page is refreshed, the browser loads the original HTML and CSS again, so a temporary JavaScript-only DOM change is normally lost unless the application stores the change somewhere persistent.

```text
JavaScript changes DOM
        ↓
Current page changes
        ↓
Refresh
        ↓
Original document is loaded again
        ↓
Temporary DOM change disappears
```

### Events

JavaScript can react to user actions such as clicks.

```js
const button = document.querySelector("#submit-btn");

button.addEventListener("click", function () {
  button.textContent = "Submitted!";
});
```

The general pattern is:

```js
element.addEventListener("event", function () {
  // code to run
});
```

Common events:

```text
click
input
change
submit
mouseover
keydown
```

---

## Values and Data Types

JavaScript works with different kinds of values.

| Type | Example |
| --- | --- |
| String | `"hello"` |
| Number | `42`, `3.14` |
| Boolean | `true`, `false` |
| Undefined | `undefined` |
| Null | `null` |

### `typeof`

The `typeof` operator can inspect the type of a value.

```js
typeof "hello";   // "string"
typeof 42;        // "number"
typeof true;      // "boolean"
typeof undefined; // "undefined"
```

A well-known JavaScript behavior is:

```js
typeof null; // "object"
```

This is a historical JavaScript quirk.

Arrays and ordinary objects also report:

```js
typeof [1, 2, 3]; // "object"
typeof {};        // "object"
```

### Strings

A string represents text.

JavaScript supports:

```js
"double quotes";
'single quotes';
`template literals`;
```

Example:

```js
const greeting = "Hello";

console.log(greeting.length);
console.log(greeting[0]);
```

Output:

```text
5
H
```

String indexes start at `0`.

```text
H e l l o
0 1 2 3 4
```

### Useful String Methods

```js
const phrase = "JavaScript is fun";

phrase.length;
phrase.indexOf("is");
phrase.includes("fun");
phrase.startsWith("Java");
phrase.toLowerCase();
```

Strings are primitive values. Methods such as `.toUpperCase()` return a new value instead of changing the original string automatically.

```js
const word = "hello";

word.toUpperCase();

console.log(word); // "hello"
```

---

## Operators

Operators allow JavaScript to perform calculations and comparisons.

### Arithmetic Operators

```js
5 + 3;  // 8
5 - 3;  // 2
5 * 3;  // 15
5 / 3;  // 1.666...
5 % 3;  // 2
2 ** 3; // 8
```

| Operator | Meaning |
| --- | --- |
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Remainder / modulo |
| `**` | Exponentiation |

### Comparison Operators

Comparison operators produce a boolean result.

```js
5 > 3;  // true
5 < 3;  // false
5 >= 5; // true
5 <= 4; // false
```

### Equality

Loose equality can convert types before comparing.

```js
5 == "5"; // true
```

Strict equality checks both value and type.

```js
5 === "5"; // false
5 !== "5"; // true
```

Best practice: prefer `===` and `!==` because strict comparisons reduce unexpected type conversion.

---

## Expressions and Variables

An expression is a piece of code that produces a value.

```js
3 + 4;     // 7
"a" + "b"; // "ab"
age > 18; // true or false
```

### Declaring and Assigning Variables

A variable can be declared first and assigned later:

```js
let age;

age = 20;
```

Or both can happen together:

```js
let name = "Ali";
```

### `let`

`let` allows a variable to be reassigned.

```js
let age = 20;
age = 21;
```

### `const`

`const` requires an initial value and prevents reassignment of the variable.

```js
const pi = 3.14159;
```

This is not allowed:

```js
pi = 4; // TypeError
```

### Statements vs Expressions

An expression produces a value:

```js
3 + 4;
age > 18;
```

A statement performs an action or controls execution.

```js
if (age > 18) {
  console.log("adult");
}
```

---

## Arrays

An array is an ordered collection of values.

Indexes start at `0`.

```js
const fruits = ["apple", "banana", "cherry"];

console.log(fruits[0]);
console.log(fruits.length);
```

Output:

```text
apple
3
```

Array indexes:

```text
apple   banana   cherry
  0       1        2
```

### Useful Array Methods

```js
const nums = [1, 2, 3];

nums.push(4);       // add to end
nums.pop();         // remove from end
nums.unshift(0);    // add to beginning
nums.shift();       // remove from beginning
nums.includes(2);   // check for value
nums.join("-");     // combine into string
nums.slice(0, 2);   // copy part of array
```

### Array Mutability and `const`

`const` prevents reassignment of the variable, but it does not make the contents of an array immutable.

This is allowed:

```js
const colors = ["red", "green"];

colors.push("blue");
```

This is not allowed:

```js
colors = ["yellow"];
```

### Shared References

```js
let array1 = [1, 2, 3];
let array2 = array1;

array1[1] = 4;

console.log(array1); // [1, 4, 3]
console.log(array2); // [1, 4, 3]
```

Both variables refer to the same array.

```text
array1 ───────┐
              ↓
          [1, 4, 3]
              ↑
array2 ───────┘
```

---

## Objects

Objects group related values together using properties.

```js
const js = {
  name: "JavaScript",
  abbreviation: "JS",
  isAwesome: true,
  officialSpec: "ECMAScript",
  birthYear: 1995,
  creator: "Brendan Eich"
};
```

A property has a key and a value:

```text
name -> "JavaScript"
abbreviation -> "JS"
birthYear -> 1995
```

### Accessing Object Properties

```js
console.log(js.name); // JavaScript
console.log(js.birthYear);
```

### Modifying and Adding Properties

```js
const indecisive = {
  lunch: "sandwich"
};

indecisive.lunch = "tacos";
indecisive.snack = "chips";
```

### Objects and Arrays

Arrays are objects in JavaScript.

```js
typeof { snack: "chips" }; // "object"
typeof ["chips"];          // "object"
```

Arrays have special behavior and methods designed for ordered collections.

### Nested Objects and Arrays

```js
const anjana = {
  name: "Anjana",
  home: "San Francisco",
  languages: ["English", "German", "French"],
  pet: null,
  vehicle: "Vespa",
  hobbies: ["travel", "climbing", "gaming", "lindy hop"]
};

anjana.languages[0];
anjana.hobbies[2];
```

Another example:

```js
const menu = {
  lunch: {
    appetizer: "salad",
    main: "spaghetti",
    dessert: "tiramisu"
  },
  dinner: {
    appetizer: "samosa",
    main: "saag paneer",
    dessert: "gulab jamun"
  }
};

const tiramisu = menu.lunch.dessert;
```

### Object Methods

A function stored as an object property is called a method.

```js
const dog = {
  name: "Ein",
  breed: "Corgi",

  speak: function () {
    console.log("woof woof");
  }
};

dog.speak();
```

### The `this` Keyword

Inside an object method, `this` can refer to the object on which the method is called.

```js
const user = {
  name: "Ali",

  greet: function () {
    console.log("Hi my name is", this.name);
  }
};

user.greet();
```

### Built-In Objects

JavaScript provides built-in objects and utilities.

```js
Math.max(3, 7, 2); // 7
Math.round(4.6);   // 5

const now = new Date();

JSON.stringify({ a: 1 }); // '{"a":1}'
```

### `Object.freeze()`

`Object.freeze()` prevents changes to an object's own existing properties. It prevents adding, changing, or deleting those properties.

```js
const user = {
  name: "Ali",
  age: 22
};

Object.freeze(user);

user.name = "Omar";

console.log(user.name); // "Ali"
console.log(Object.isFrozen(user)); // true
```

#### `const` vs `Object.freeze()`

These are different:

```js
const user = {
  name: "Ali"
};

user.name = "Omar"; // allowed
```

`const` prevents reassignment of the variable reference. `Object.freeze()` prevents changes to the object's own properties.

#### Shallow Freeze

`Object.freeze()` is shallow. A nested object is not automatically frozen.

```js
const user = {
  name: "Ali",
  address: {
    city: "Jenin"
  }
};

Object.freeze(user);

user.address.city = "Nablus"; // nested object can still change
```

---

## Functions

Functions allow us to group reusable instructions.

### Basic Function

```js
function greet() {
  console.log("Hello!");
}

greet();
```

### Parameters and Arguments

A function can receive information through parameters.

```js
function greet(name) {
  console.log("Hello " + name);
}

greet("Reem");
```

Here:

- `name` is the parameter.
- `"Reem"` is the argument.

### Multiple Parameters

```js
function add(a, b) {
  return a + b;
}

const result = add(3, 4);

console.log(result); // 7
```

### Fewer Arguments Than Parameters

JavaScript allows a function to be called with fewer arguments than the number of declared parameters.

```js
function add(a, b) {
  return a + b;
}

console.log(add(5));
```

The values are:

```text
a -> 5
b -> undefined
```

Therefore:

```text
5 + undefined -> NaN
```

JavaScript does not automatically throw an error simply because an argument is missing. The missing parameter receives `undefined`.

### Function Returning a Value

```js
function square(number) {
  return number * number;
}

const result = square(5);

console.log(result); // 25
```

---

## Quiz Project

The quiz project brings several concepts together.

It uses:

- Variables.
- Data types.
- Operators.
- Conditional logic.
- Functions.
- DOM selection.
- DOM updates.
- User input.

### Project Setup

```text
quiz-project/
├── index.html
├── style.css
└── script.js
```

HTML:

```html
<p id="result"></p>
<p id="message"></p>

<script src="script.js"></script>
```

JavaScript:

```js
const result = document.querySelector("#result");
const score = 8;

result.textContent = "Your score: " + score;
```

### Conditional Result

```js
const message = document.querySelector("#message");

if (score >= 5) {
  message.textContent = "You passed!";
} else {
  message.textContent = "Try again!";
}
```

This demonstrates:

```text
Variable
   ↓
Condition
   ↓
Decision
   ↓
DOM update
```

### `getMultipleChoices`

A quiz application can use a function such as `getMultipleChoices` to obtain or process the multiple-choice options used by the quiz.

The important concept is that functions allow repeated quiz logic to be organized into reusable blocks rather than writing the same code repeatedly.

Illustrative example:

```js
function getMultipleChoices(choices, count) {
  const selected = [];

  while (selected.length < count) {
    selected.push(choices[selected.length]);
  }

  return selected;
}

const choices = ["A", "B", "C", "D"];
const result = getMultipleChoices(choices, 3);

console.log(result); // ["A", "B", "C"]
```

---

## Tic Tac Toe

Tic Tac Toe demonstrates how several JavaScript concepts work together:

- Arrays.
- Objects/functions when needed.
- Events.
- DOM manipulation.
- User interaction.
- Updating application state.

A simple board can be represented by an array:

```js
const board = [
  "", "", "",
  "", "", "",
  "", "", ""
];
```

The center square is index `4`.

```js
board[4] = "X";
```

The data now represents:

```text
|   |   |   |
|---|---|---|
|   | X |   |
|---|---|---|
|   |   |   |
```

Data and UI flow:

```text
User clicks a square
        ↓
JavaScript receives the event
        ↓
Board array is updated
        ↓
The DOM is updated
        ↓
User sees the new board
```

The array represents the application data, while the DOM represents what the user sees.

---

## Day 2: DOM, Objects, Functions, APIs, and Async JavaScript

Day 2 connects JavaScript logic to the DOM and introduces asynchronous work with timers and APIs.

### Day 2 Topics

- Selecting an HTML element by ID.
- Selecting elements by tag name.
- Selecting elements by class name.
- Using `.length` with DOM collections.
- Reading and setting `.textContent`.
- Understanding what happens to temporary DOM changes after refresh.
- Understanding `Object.freeze()`.
- Understanding missing function arguments.
- Understanding the purpose of `getMultipleChoices`.
- Using `setTimeout()`.
- Understanding the Dog CEO API.
- Extracting properties from API response objects.
- Understanding promises, `fetch()`, and `await`.
- Using object and array destructuring.
- Naming an array after splitting a URL.
- Splitting a Dog CEO image URL and reading a specific index.

### `setTimeout()`

`setTimeout()` schedules a callback function to run later. JavaScript continues executing synchronous code while the timer waits.

```js
console.log("first");

setTimeout(() => {
  console.log("third");
}, 1000);

console.log("second");
```

Typical output:

```text
first
second
third
```

The delay is measured in milliseconds:

```js
setTimeout(callback, 1000); // about one second
```

### Dog CEO API

An API provides a way for an application to request data from another system.

Example endpoint:

```text
https://dog.ceo/api/breed/hound/list
```

Example response:

```json
{
  "message": [
    "afghan",
    "basset",
    "blood",
    "english",
    "ibizan",
    "plott",
    "walker"
  ],
  "status": "success"
}
```

Important parts:

| Property | Meaning |
| --- | --- |
| `message` | Array of breeds |
| `status` | Request status |

### Promises, `fetch()`, and `await`

Network requests take time, so `fetch()` returns a promise.

```js
const response = await fetch("https://dog.ceo/api/breed/hound/list");
```

The response is a `Response` object. Its body can be parsed as JSON:

```js
const body = await response.json();
```

`response.json()` also returns a promise, so `await` is used again.

`await` is normally used inside an `async` function:

```js
async function fetchResponse(url) {
  const response = await fetch(url);
  return response;
}
```

Overall flow:

```text
fetch(url)
    ↓
Promise
    ↓
await
    ↓
Response
    ↓
response.json()
    ↓
Promise
    ↓
await
    ↓
JavaScript data
```

### Destructuring

Destructuring extracts values from objects or arrays into variables.

#### Object Destructuring

```js
const data = {
  id: 10,
  name: "JavaScript"
};

const { id, name } = data;
```

Now:

```text
id   -> 10
name -> "JavaScript"
```

Dog CEO example:

```js
const body = await response.json();
const { message } = body;
```

Now `message` contains the array from the API response.

#### Array Destructuring

```js
const [first, second, third] = ["A", "B", "C"];
```

Results:

```text
first  -> "A"
second -> "B"
third  -> "C"
```

You can skip values:

```js
const [, , third] = ["A", "B", "C"];
```

You can collect remaining values with rest syntax:

```js
const [first, ...rest] = ["A", "B", "C"];
```

Results:

```text
first -> "A"
rest  -> ["B", "C"]
```

### Splitting a Dog CEO URL

Given this URL:

```text
https://images.dog.ceo/breeds/poodle-standard
```

Using `.split("/")`:

```js
const url = "https://images.dog.ceo/breeds/poodle-standard";
const parts = url.split("/");

console.log(parts);
```

The resulting array is:

| Index | Value |
| --- | --- |
| `0` | `"https:"` |
| `1` | `""` |
| `2` | `"images.dog.ceo"` |
| `3` | `"breeds"` |
| `4` | `"poodle-standard"` |

The empty value at index `1` comes from the double slash in `https://`.

Extract the breed:

```js
const breed = parts[4];

console.log(breed); // "poodle-standard"
```

Naming the result something like `urlArray` can make it clear that the variable now contains an array rather than the original string.

```js
const urlArray = url.split("/");
```

### Complete Day 2 Example

HTML:

```html
<h1 id="title">Doggo Fetch</h1>
<button id="loadButton">Load Breeds</button>
<p id="status"></p>
<ul id="breeds"></ul>
```

JavaScript:

```js
const title = document.getElementById("title");
const button = document.getElementById("loadButton");
const status = document.getElementById("status");
const breedsList = document.getElementById("breeds");

title.textContent = "Dog Breeds";

async function loadBreeds() {
  status.textContent = "Loading...";

  const response = await fetch("https://dog.ceo/api/breed/hound/list");
  const body = await response.json();
  const { message } = body;

  status.textContent = `${message.length} breeds found.`;
  breedsList.textContent = "";

  for (const breed of message) {
    const li = document.createElement("li");
    li.textContent = breed;
    breedsList.appendChild(li);
  }
}

button.addEventListener("click", loadBreeds);
```

Flow:

1. Select elements from the DOM.
2. User clicks the button.
3. The async function starts.
4. `fetch()` requests API data.
5. `await` waits for the promise.
6. `response.json()` parses the response body.
7. Destructuring extracts `message`.
8. `.length` counts the breeds.
9. `.textContent` updates the page.
10. The breeds are added to the DOM.

### Final Day 2 Mental Model

```text
HTML
  ↓
DOM
  ↓
Select elements
  ↓
Read / change content
  ↓
Functions organize logic
  ↓
setTimeout / async operations happen later
  ↓
fetch() requests API data
  ↓
await waits for Promises
  ↓
Destructuring extracts useful data
  ↓
DOM is updated with the result
  ↓
Interactive web page
```

---

## JavaScript + DOM Mental Model

The most important idea in the course is the relationship between data, logic, and the page.

```text
             JavaScript
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
     Data      Logic      DOM
       │         │         │
 arrays/objects  functions  HTML
 variables      conditions  elements
       │         │         │
       └─────────┼─────────┘
                 ↓
          Interactive Page
```

---

## Quick Reference

### DOM

```js
document.querySelector("h1");
document.querySelectorAll("p");
document.getElementById("title");
document.getElementsByTagName("li");
document.getElementsByClassName("card");
```

### DOM Content

```js
element.textContent;
element.textContent = "New text";
```

### Events

```js
element.addEventListener("click", function () {
  // action
});
```

### Data Types

```js
typeof "text";
typeof 42;
typeof true;
typeof undefined;
typeof null;
```

### Strings

```js
text.length;
text[0];
text.indexOf("x");
text.includes("x");
text.startsWith("x");
text.toLowerCase();
```

### Operators

```js
+  -  *  /  %  **
>  <  >=  <=
=== !==
```

### Variables

```js
let age = 20;
const name = "Ali";
```

### Arrays

```js
array[0];
array.length;
array.push(value);
array.pop();
array.unshift(value);
array.shift();
array.includes(value);
array.join("-");
array.slice(0, 2);
```

### Objects

```js
object.property;
object.property = value;
object.newProperty = value;
Object.freeze(object);
Object.isFrozen(object);
```

### Methods and `this`

```js
const user = {
  name: "Ali",

  greet: function () {
    console.log(this.name);
  }
};

user.greet();
```

### Functions

```js
function greet(name) {
  console.log("Hello " + name);
}

greet("Reem");
```

### Timer

```js
setTimeout(callback, 1000);
```

### Fetch and JSON

```js
const response = await fetch(url);
const body = await response.json();
```

### Destructuring

```js
const { message } = body;
const [first, second] = array;
```

### String Splitting

```js
const parts = url.split("/");
```

---

## Common Beginner Mistakes

### 1. Forgetting That Array Indexes Start at 0

```js
const fruits = ["apple", "banana", "cherry"];

fruits[0]; // apple
fruits[1]; // banana
fruits[2]; // cherry
```

### 2. Confusing `=` with `===`

`=` is used for assignment.

```js
let score = 10;
```

`===` is used for strict equality comparison.

```js
score === 10;
```

### 3. Thinking `const` Makes an Array or Object Immutable

This is allowed:

```js
const numbers = [1, 2];

numbers.push(3);
```

But this is not:

```js
numbers = [4, 5];
```

Use `Object.freeze()` when you want to prevent changes to an object's own properties.

### 4. Forgetting That Objects and Arrays Are Reference Values

```js
let a = [1, 2, 3];
let b = a;

b[0] = 99;

console.log(a); // [99, 2, 3]
```

`a` is also changed because both variables refer to the same array.

### 5. Selecting an Element That Does Not Exist

```js
const button = document.querySelector("#submit-btn");
```

If the page does not contain that element, `button` can be `null`.

Always make sure the selector matches an existing HTML element.

### 6. Forgetting That Missing Function Arguments Become `undefined`

```js
function add(a, b) {
  return a + b;
}

add(5); // b is undefined, result is NaN
```

### 7. Forgetting That `response.json()` Also Needs `await`

```js
const response = await fetch(url);
const body = await response.json();
```

Both `fetch()` and `response.json()` return promises.

---

## Practice Checklist

### JavaScript Basics

- [ ] I can explain what JavaScript is.
- [ ] I can run JavaScript in the browser console.
- [ ] I know how to connect an external `.js` file.

### DOM

- [ ] I can use `querySelector()`.
- [ ] I can use `querySelectorAll()`.
- [ ] I can use `getElementById()`.
- [ ] I can use `getElementsByTagName()`.
- [ ] I can use `getElementsByClassName()`.
- [ ] I understand `.length` for DOM collections.
- [ ] I can read and change `.textContent`.
- [ ] I can respond to a click with `addEventListener()`.
- [ ] I understand why a temporary DOM change normally disappears after refresh.

### Data Types

- [ ] I know string, number, boolean, undefined, and null.
- [ ] I can use `typeof`.
- [ ] I understand the `typeof null === "object"` behavior.

### Operators

- [ ] I can perform arithmetic.
- [ ] I understand `%`.
- [ ] I understand `==` vs `===`.
- [ ] I understand `!=` vs `!==`.

### Variables and Expressions

- [ ] I understand declaration and assignment.
- [ ] I know when to use `let`.
- [ ] I know when to use `const`.
- [ ] I can distinguish expressions from statements.

### Arrays

- [ ] I know that indexes start at `0`.
- [ ] I can use `push()` and `pop()`.
- [ ] I can use `shift()` and `unshift()`.
- [ ] I can use `includes()`.
- [ ] I can use `join()`.
- [ ] I understand `slice()`.
- [ ] I understand shared references.
- [ ] I understand that `const` does not freeze an array.
- [ ] I can use array destructuring.

### Objects

- [ ] I can create an object.
- [ ] I can access properties.
- [ ] I can modify properties.
- [ ] I can add properties.
- [ ] I understand methods.
- [ ] I understand `this`.
- [ ] I can access nested objects and arrays.
- [ ] I understand `Object.freeze()`.
- [ ] I understand the difference between `const` and `Object.freeze()`.
- [ ] I understand shallow freeze.
- [ ] I can use object destructuring.

### Functions

- [ ] I can declare a function.
- [ ] I can call a function.
- [ ] I understand parameters and arguments.
- [ ] I understand `return`.
- [ ] I know what happens when an argument is missing.
- [ ] I understand the purpose of `getMultipleChoices` and its while-loop idea.

### Asynchronous JavaScript and APIs

- [ ] I understand what `setTimeout()` does.
- [ ] I understand why `fetch()` returns a promise.
- [ ] I can use `await` inside an `async` function.
- [ ] I can parse a response with `response.json()`.
- [ ] I can extract a property with object destructuring.
- [ ] I can split a URL with `.split("/")`.
- [ ] I understand the indexes in the Dog CEO URL example.

### Projects

- [ ] I can connect JavaScript to HTML.
- [ ] I can update a page based on a variable.
- [ ] I can use a condition to display a result.
- [ ] I understand the basic data flow of a quiz.
- [ ] I understand how Tic Tac Toe can store board state in an array.
- [ ] I can combine DOM selection, functions, async code, API data, and DOM updates.

---

## Final Summary

| Section | Main Idea |
| --- | --- |
| Getting Started | JavaScript adds behavior and interactivity to web pages |
| DOM | JavaScript can read and change HTML elements |
| Values and Data Types | JavaScript works with different types of values |
| Strings | Text values provide useful properties and methods |
| Operators | Operators perform calculations and comparisons |
| Expressions | Expressions produce values |
| Variables | Variables provide named references to values |
| Arrays | Arrays store ordered collections of values |
| Mutability | `const` protects reassignment, not array/object contents |
| Objects | Objects group related data through properties |
| Methods | Functions stored on objects are methods |
| `this` | `this` can refer to the object used to call a method |
| Functions | Functions organize reusable logic |
| Quiz Project | Combines variables, logic, functions, and DOM manipulation |
| Tic Tac Toe | Demonstrates state, events, arrays, and DOM updates |
| Timers | `setTimeout()` schedules work for later |
| APIs | APIs let JavaScript request data from another system |
| Promises | Promises represent values that may be available later |
| `fetch()` and `await` | Used to request and wait for API data |
| Destructuring | Extracts useful values from objects and arrays |
