
# JavaScript First Steps — Day 1

## Table of Contents

1. [Day 1 Overview](#1-day-1-overview)
2. [What is JavaScript?](#2-what-is-javascript)
3. [Where to Write JavaScript](#3-where-to-write-javascript)
4. [DOM: Document Object Model](#4-dom-document-object-model)
5. [Selecting Elements](#5-selecting-elements)
6. [Reading and Changing Content](#6-reading-and-changing-content)
7. [Changing a Web Page](#7-changing-a-web-page)
8. [Events](#8-events)
9. [Values and Data Types](#9-values-and-data-types)
10. [Strings](#10-strings)
11. [Operators](#11-operators)
12. [Expressions and Variables](#12-expressions-and-variables)
13. [Arrays](#13-arrays)
14. [Array Mutability and References](#14-array-mutability-and-references)
15. [Objects](#15-objects)
16. [Nested Objects and Arrays](#16-nested-objects-and-arrays)
17. [Object Methods and `this`](#17-object-methods-and-this)
18. [`Object.freeze()`](#18-objectfreeze)
19. [Functions](#19-functions)
20. [Quiz Project](#20-quiz-project)
21. [Tic Tac Toe](#21-tic-tac-toe)
22. [`setTimeout()` and Async Basics](#22-settimeout-and-async-basics)
23. [APIs, Promises, `fetch()`, and `await`](#23-apis-promises-fetch-and-await)
24. [Destructuring](#24-destructuring)
25. [Splitting URLs](#25-splitting-urls)
26. [Complete Day 1 Example](#26-complete-day-1-example)
27. [JavaScript + DOM Mental Model](#27-javascript--dom-mental-model)
28. [Quick Reference](#28-quick-reference)
29. [Common Beginner Mistakes](#29-common-beginner-mistakes)
30. [Practice Checklist](#30-practice-checklist)

---

## 1. Day 1 Overview

Day 1 was basically the "here's what JavaScript actually is" day. HTML gives structure, CSS gives style, and JavaScript is the thing that makes a page *do* something.

The main topics covered:

- What JavaScript is and how to run it
- The browser console
- The DOM (Document Object Model)
- Selecting and changing HTML elements
- Values and data types (strings, numbers, booleans, `undefined`, `null`)
- Operators
- Variables (`let` and `const`)
- Arrays
- Objects
- Functions
- Small projects (Quiz and Tic Tac Toe)
- Timers, APIs, promises, `fetch()`, `await`
- Destructuring
- URL processing

By the end of Day 1, the goal is to understand how JavaScript represents data and how that data can be used to control a web page.

The big picture:

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

The goal isn't just memorizing syntax — it's understanding how JavaScript represents data and uses it to control a page.

---

## 2. What is JavaScript?

JavaScript is a high-level, dynamically typed programming language. It's used in browsers to make pages interactive, but it can also run outside the browser through environments like Node.js.

JavaScript can:

- Read HTML elements
- Change text and styles
- React to user actions
- Store and process data
- Perform calculations
- Work with arrays and objects
- Create reusable functions
- Communicate with other systems

JavaScript is standardized as ECMAScript. It was created in 1995 by Brendan Eich (allegedly in about 10 days, which explains some of its quirks).

### First JavaScript Statement

```js
console.log("Hello, JavaScript!");
```

`console.log()` prints a value or message to the browser console. This is probably the most-used function in all of JavaScript, especially when debugging.

---

## 3. Where to Write JavaScript

There are three common ways to run JavaScript.

### 1. Browser DevTools Console

The console is great for quick experiments.

```text
Right-click → Inspect → Console
```

Then try:

```js
console.log("Hello!");
```

### 2. Inline JavaScript

JavaScript can go directly inside an HTML `<script>` element.

```html
<script>
  console.log("Hello from inline JavaScript");
</script>
```

### 3. External JavaScript File

A separate `.js` file can be linked to an HTML page.

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

Keeping HTML, CSS, and JavaScript separated makes projects easier to organize. It's tempting to jam everything into one file when starting out, but it gets messy fast.

---

## 4. DOM: Document Object Model

The DOM is the browser's representation of an HTML document. Basically, the browser turns HTML elements into objects that JavaScript can access and manipulate.

```text
document
└── html
    ├── head
    └── body
        ├── h1
        └── p
```

Through the DOM, JavaScript can:

- Find elements
- Read their content
- Change their content
- Change styles
- Add or remove classes
- Respond to user events

---

## 5. Selecting Elements

Before changing anything, you have to select it first. There are several methods for this.

### `querySelector()`

Selects the **first** element that matches a CSS selector.

```js
const title = document.querySelector("h1");
```

It works with IDs and classes too:

```js
document.querySelector("#title");
document.querySelector(".card");
```

### `querySelectorAll()`

Selects **all** elements that match a CSS selector.

```js
const paragraphs = document.querySelectorAll("p");
```

The result is a `NodeList`, which is similar to an array but not exactly one.

### `getElementById()`

Selects an element using its ID.

```js
const title = document.getElementById("title");
```

The ID is passed without the `#`.

```js
document.getElementById("title"); // correct — no #
document.querySelector("#title"); // correct — with #
```

### `getElementsByTagName()`

Selects elements by tag name.

```js
const items = document.getElementsByTagName("li");
```

### `getElementsByClassName()`

Selects elements by class name.

```js
const cards = document.getElementsByClassName("card");
```

### Selection Comparison

| Method                     | Purpose                             |
| -------------------------- | ----------------------------------- |
| `getElementById()`         | Select one element by ID            |
| `getElementsByTagName()`   | Select elements by tag name         |
| `getElementsByClassName()` | Select elements by class name       |
| `querySelector()`          | Select the first CSS selector match |
| `querySelectorAll()`       | Select all CSS selector matches     |

In practice, `querySelector()` and `querySelectorAll()` are the most flexible and are used most often.

### `.length` with DOM Collections

`.length` gives the number of items in a collection.

```js
const items = document.querySelectorAll("li");
console.log(items.length);
```

Same idea with class selections:

```js
const buttons = document.getElementsByClassName("choice");
console.log(buttons.length);
```

---

## 6. Reading and Changing Content

### `.textContent`

`.textContent` reads or changes the text inside an element.

Reading:

```js
const title = document.querySelector("h1");
console.log(title.textContent);
```

Changing:

```js
title.textContent = "New Title";
```

It's a property, not a function:

```js
title.textContent = "New text"; // correct
title.textContent();            // incorrect — throws an error
```

No parentheses. Just assignment.

---

## 7. Changing a Web Page

Once an element is selected, JavaScript can modify it in all sorts of ways:

```js
const title = document.querySelector("h1");

title.textContent = "New Title";
title.style.color = "blue";
title.classList.add("highlight");
```

### DOM Refresh Behavior

DOM changes made by JavaScript affect the *current* page in memory only.

```js
document.body.style.backgroundColor = "black";
```

If the page gets refreshed, the browser reloads the original HTML and CSS, so any temporary JavaScript-only DOM changes disappear unless the app saves them somewhere persistent (like localStorage or a database).

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

This confused me at first — I thought once I changed something with JS it would stick. It doesn't.

---

## 8. Events

Events are things that happen in the browser — clicks, hovers, key presses, form submissions, etc. JavaScript can react to them using `addEventListener()`.

```js
const button = document.querySelector("#submit-btn");

button.addEventListener("click", function () {
  button.textContent = "Submitted!";
});
```

General pattern:

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

Events are covered more deeply in Day 2, but this is the basic idea.

---

## 9. Values and Data Types

JavaScript works with different kinds of values.

| Type      | Example         |
| --------- | --------------- |
| String    | `"hello"`       |
| Number    | `42`, `3.14`    |
| Boolean   | `true`, `false` |
| Undefined | `undefined`     |
| Null      | `null`          |

### `typeof`

The `typeof` operator tells you the type of a value.

```js
typeof "hello";   // "string"
typeof 42;        // "number"
typeof true;      // "boolean"
typeof undefined; // "undefined"
```

There's a famous JavaScript quirk:

```js
typeof null; // "object"
```

This is technically a bug from the original language design that was never fixed because it would break too much existing code. Just something to know.

Arrays and ordinary objects also return `"object"`:

```js
typeof [1, 2, 3]; // "object"
typeof {};        // "object"
```

---

## 10. Strings

A string represents text.

JavaScript supports three ways to write them:

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

String indexes start at `0`:

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

Strings are **primitive** values. Methods like `.toUpperCase()` return a *new* value instead of changing the original.

```js
const word = "hello";

word.toUpperCase();

console.log(word); // "hello" — unchanged
```

To actually use the result, you have to store it:

```js
const upper = word.toUpperCase();
console.log(upper); // "HELLO"
```

---

## 11. Operators

Operators let JavaScript do calculations and comparisons.

### Arithmetic Operators

```js
5 + 3;  // 8
5 - 3;  // 2
5 * 3;  // 15
5 / 3;  // 1.666...
5 % 3;  // 2
2 ** 3; // 8
```

| Operator | Meaning            |
| -------- | ------------------ |
| `+`      | Addition           |
| `-`      | Subtraction        |
| `*`      | Multiplication     |
| `/`      | Division           |
| `%`      | Remainder / modulo |
| `**`     | Exponentiation     |

### Comparison Operators

Comparisons return a boolean.

```js
5 > 3;  // true
5 < 3;  // false
5 >= 5; // true
5 <= 4; // false
```

### Equality

Loose equality (`==`) converts types before comparing:

```js
5 == "5"; // true
```

Strict equality (`===`) checks both value **and** type:

```js
5 === "5"; // false
5 !== "5"; // true
```

**Best practice:** always use `===` and `!==`. Loose equality causes weird bugs because of automatic type conversion.

---

## 12. Expressions and Variables

An expression is a piece of code that produces a value.

```js
3 + 4;     // 7
"a" + "b"; // "ab"
age > 18;  // true or false
```

### Declaring and Assigning Variables

Declare first, assign later:

```js
let age;
age = 20;
```

Or both at once:

```js
let name = "Ali";
```

### `let`

`let` allows reassignment:

```js
let age = 20;
age = 21;
```

### `const`

`const` requires an initial value and prevents reassignment:

```js
const pi = 3.14159;
```

This throws an error:

```js
pi = 4; // TypeError
```

### Statements vs Expressions

An expression produces a value:

```js
3 + 4;
age > 18;
```

A statement performs an action or controls execution:

```js
if (age > 18) {
  console.log("adult");
}
```

The distinction sounds nitpicky but comes up a lot when reading docs or error messages.

---

## 13. Arrays

An array is an ordered collection of values. Indexes start at `0`.

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

Visualizing indexes:

```text
apple   banana   cherry
  0       1        2
```

### Useful Array Methods

```js
const nums = [1, 2, 3];

nums.push(4);     // add to end
nums.pop();       // remove from end
nums.unshift(0);  // add to beginning
nums.shift();     // remove from beginning
nums.includes(2); // check for value
nums.join("-");   // combine into string
nums.slice(0, 2); // copy part of array
```

---

## 14. Array Mutability and References

### `const` Doesn't Freeze Arrays

`const` prevents reassignment of the variable, but not changes to the contents.

Allowed:

```js
const colors = ["red", "green"];
colors.push("blue"); // works fine
```

Not allowed:

```js
colors = ["yellow"]; // TypeError
```

This tripped me up. I thought `const` meant "totally locked" but it doesn't.

### Shared References

```js
let array1 = [1, 2, 3];
let array2 = array1;

array1[1] = 4;

console.log(array1); // [1, 4, 3]
console.log(array2); // [1, 4, 3]
```

Both variables refer to the **same** array. Changing one changes the other.

```text
array1 ───────┐
              ↓
          [1, 4, 3]
              ↑
array2 ───────┘
```

This is really important to remember. Arrays and objects are passed by reference, not by copy.

---

## 15. Objects

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

Each property has a key and a value:

```text
name         → "JavaScript"
abbreviation → "JS"
birthYear    → 1995
```

### Accessing Properties

```js
console.log(js.name);      // "JavaScript"
console.log(js.birthYear); // 1995
```

### Modifying and Adding Properties

```js
const indecisive = {
  lunch: "sandwich"
};

indecisive.lunch = "tacos";   // change
indecisive.snack = "chips";   // add new
```

### Objects and Arrays

Arrays are actually objects in JavaScript:

```js
typeof { snack: "chips" }; // "object"
typeof ["chips"];          // "object"
```

Arrays just have special behavior and methods designed for ordered collections.

---

## 16. Nested Objects and Arrays

Objects can contain other objects and arrays. This is where things get interesting.

```js
const anjana = {
  name: "Anjana",
  home: "San Francisco",
  languages: ["English", "German", "French"],
  pet: null,
  vehicle: "Vespa",
  hobbies: ["travel", "climbing", "gaming", "lindy hop"]
};

anjana.languages[0]; // "English"
anjana.hobbies[2];   // "gaming"
```

Another example with nested objects:

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

You just chain the accessors: `menu.lunch.dessert`. Nice and readable.

---

## 17. Object Methods and `this`

A function stored as an object property is called a **method**.

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

Inside a method, `this` refers to the object the method was called on.

```js
const user = {
  name: "Ali",

  greet: function () {
    console.log("Hi my name is", this.name);
  }
};

user.greet(); // "Hi my name is Ali"
```

`this` is one of those concepts that gets more complicated later, but at this level it's pretty straightforward — it's the object you're inside of.

### Built-In Objects

JavaScript has a bunch of built-in objects and utilities:

```js
Math.max(3, 7, 2); // 7
Math.round(4.6);   // 5

const now = new Date();

JSON.stringify({ a: 1 }); // '{"a":1}'
```

---

## 18. `Object.freeze()`

`Object.freeze()` prevents changes to an object's own existing properties — no adding, changing, or deleting.

```js
const user = {
  name: "Ali",
  age: 22
};

Object.freeze(user);

user.name = "Omar";

console.log(user.name);            // "Ali"
console.log(Object.isFrozen(user)); // true
```

### `const` vs `Object.freeze()`

Very different things:

```js
const user = {
  name: "Ali"
};

user.name = "Omar"; // allowed — const doesn't freeze contents
```

- `const` prevents reassignment of the variable
- `Object.freeze()` prevents changes to the object's properties

### Shallow Freeze

`Object.freeze()` is shallow — nested objects are **not** frozen automatically.

```js
const user = {
  name: "Ali",
  address: {
    city: "Jenin"
  }
};

Object.freeze(user);

user.address.city = "Nablus"; // still works!
```

If you need deep freezing, you have to freeze each nested object manually (or write a helper function).

---

## 19. Functions

Functions group reusable instructions into a single unit.

### Basic Function

```js
function greet() {
  console.log("Hello!");
}

greet();
```

### Parameters and Arguments

Parameters are placeholders. Arguments are the actual values passed in.

```js
function greet(name) {
  console.log("Hello " + name);
}

greet("Reem");
```

- `name` is the parameter
- `"Reem"` is the argument

### Multiple Parameters

```js
function add(a, b) {
  return a + b;
}

const result = add(3, 4);
console.log(result); // 7
```

### Fewer Arguments Than Parameters

JavaScript doesn't complain if you leave out arguments. Missing ones just become `undefined`.

```js
function add(a, b) {
  return a + b;
}

console.log(add(5));
```

The values become:

```text
a → 5
b → undefined
```

So:

```text
5 + undefined → NaN
```

No error is thrown. This can cause silent bugs.

### Function Returning a Value

```js
function square(number) {
  return number * number;
}

const result = square(5);
console.log(result); // 25
```

Functions are covered in more detail in Day 2, but this is enough to start.

---

## 20. Quiz Project

The quiz project pulls together a bunch of the Day 1 concepts.

It uses:

- Variables
- Data types
- Operators
- Conditional logic
- Functions
- DOM selection
- DOM updates
- User input

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

The flow:

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

The quiz uses a function like `getMultipleChoices` to build or process the multiple-choice options.

The key idea is that functions let you organize repeated logic into reusable blocks instead of copy-pasting code.

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

## 21. Tic Tac Toe

Tic Tac Toe is a classic project that shows how JavaScript concepts fit together:

- Arrays for the board
- Functions for the logic
- Events for the clicks
- DOM manipulation for the UI
- User interaction
- Updating application state

A simple board as an array:

```js
const board = [
  "", "", "",
  "", "", "",
  "", "", ""
];
```

The center square is index `4`:

```js
board[4] = "X";
```

Which represents:

```text
|   |   |   |
|---|---|---|
|   | X |   |
|---|---|---|
|   |   |   |
```

The overall flow:

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

The array is the actual data (the "state"). The DOM is what the user sees. Keeping these in sync is basically what all UI code is about.

---

## 22. `setTimeout()` and Async Basics

`setTimeout()` schedules a callback to run later. JavaScript keeps running normal code while the timer waits in the background.

```js
console.log("first");

setTimeout(() => {
  console.log("third");
}, 1000);

console.log("second");
```

Output:

```text
first
second
third
```

The delay is in milliseconds:

```js
setTimeout(callback, 1000); // about 1 second
```

This is the first hint of how JavaScript handles asynchronous code. `setTimeout` doesn't pause — the code keeps running and the callback fires later.

---

## 23. APIs, Promises, `fetch()`, and `await`

An API is basically a way for one app to request data from another system over the internet.

### Dog CEO API

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

| Property  | Meaning         |
| --------- | --------------- |
| `message` | Array of breeds |
| `status`  | Request status  |

### Promises

Network requests take time, so `fetch()` returns a **promise** — an object representing a value that will be available later.

```js
const response = await fetch("https://dog.ceo/api/breed/hound/list");
```

The result is a `Response` object. Its body needs to be parsed as JSON:

```js
const body = await response.json();
```

`response.json()` **also** returns a promise, which is why `await` is needed again. Forgetting this is a super common mistake.

### `async` Functions

`await` normally goes inside an `async` function:

```js
async function fetchResponse(url) {
  const response = await fetch(url);
  return response;
}
```

### The Full Flow

```text
fetch(url)
    ↓
Promise
    ↓ await
Response
    ↓
response.json()
    ↓
Promise
    ↓ await
JavaScript data
```

Two `await`s, one for the fetch and one for the JSON parsing.

---

## 24. Destructuring

Destructuring extracts values from objects or arrays into variables. It's a cleaner shortcut for something you'd otherwise do manually.

### Object Destructuring

```js
const data = {
  id: 10,
  name: "JavaScript"
};

const { id, name } = data;
```

Now:

```text
id   → 10
name → "JavaScript"
```

Dog CEO example:

```js
const body = await response.json();
const { message } = body;
```

Now `message` holds the array from the API response.

### Array Destructuring

```js
const [first, second, third] = ["A", "B", "C"];
```

Results:

```text
first  → "A"
second → "B"
third  → "C"
```

You can skip values with commas:

```js
const [, , third] = ["A", "B", "C"];
```

Or grab the rest with `...`:

```js
const [first, ...rest] = ["A", "B", "C"];
```

Results:

```text
first → "A"
rest  → ["B", "C"]
```

---

## 25. Splitting URLs

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

The resulting array:

| Index | Value              |
| ----- | ------------------ |
| `0`   | `"https:"`         |
| `1`   | `""`               |
| `2`   | `"images.dog.ceo"` |
| `3`   | `"breeds"`         |
| `4`   | `"poodle-standard"`|

The empty string at index `1` comes from the double slash in `https://`. That threw me off at first.

Extract the breed:

```js
const breed = parts[4];
console.log(breed); // "poodle-standard"
```

Naming the result something like `urlArray` helps signal that it's now an array, not the original string:

```js
const urlArray = url.split("/");
```

---

## 26. Complete Day 1 Example

Putting a lot of Day 1 together into one working app:

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

What's happening:

1. Select elements from the DOM
2. User clicks the button
3. Async function starts
4. `fetch()` requests API data
5. `await` waits for the promise
6. `response.json()` parses the response body
7. Destructuring extracts `message`
8. `.length` counts the breeds
9. `.textContent` updates the page
10. Breeds are added to the DOM one by one

One block of code that touches almost every Day 1 topic. That's what makes it click.

---

## 27. JavaScript + DOM Mental Model

The most important idea from Day 1 is the relationship between data, logic, and the page:

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

Data lives in variables. Logic decides what to do with it. The DOM is what the user actually sees. Everything else is just details on top of this.

---

## 28. Quick Reference

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

## 29. Common Beginner Mistakes

### 1. Forgetting That Array Indexes Start at 0

```js
const fruits = ["apple", "banana", "cherry"];

fruits[0]; // apple
fruits[1]; // banana
fruits[2]; // cherry
```

Off-by-one errors are super common at first.

### 2. Confusing `=` with `===`

`=` is assignment:

```js
let score = 10;
```

`===` is strict equality comparison:

```js
score === 10;
```

Using `=` inside an `if` is one of the classic bugs.

### 3. Thinking `const` Makes an Array or Object Immutable

Allowed:

```js
const numbers = [1, 2];
numbers.push(3);
```

Not allowed:

```js
numbers = [4, 5]; // TypeError
```

Use `Object.freeze()` when you actually want to prevent changes to an object's contents.

### 4. Forgetting That Objects and Arrays Are Reference Values

```js
let a = [1, 2, 3];
let b = a;

b[0] = 99;

console.log(a); // [99, 2, 3]
```

`a` changed too because both variables point to the same array.

### 5. Selecting an Element That Doesn't Exist

```js
const button = document.querySelector("#submit-btn");
```

If the element isn't in the HTML, `button` will be `null`. Then trying to use it throws a confusing error.

### 6. Forgetting That Missing Function Arguments Become `undefined`

```js
function add(a, b) {
  return a + b;
}

add(5); // NaN, because b is undefined
```

### 7. Forgetting That `response.json()` Also Needs `await`

```js
const response = await fetch(url);
const body = await response.json();
```

Both `fetch()` and `response.json()` return promises. Both need `await`.

---

## 30. Practice Checklist

### JavaScript Basics

- [ ] Can explain what JavaScript is
- [ ] Can run JavaScript in the browser console
- [ ] Know how to connect an external `.js` file

### DOM

- [ ] Can use `querySelector()`
- [ ] Can use `querySelectorAll()`
- [ ] Can use `getElementById()`
- [ ] Can use `getElementsByTagName()`
- [ ] Can use `getElementsByClassName()`
- [ ] Understand `.length` for DOM collections
- [ ] Can read and change `.textContent`
- [ ] Can respond to a click with `addEventListener()`
- [ ] Understand why a temporary DOM change disappears after refresh

### Data Types

- [ ] Know string, number, boolean, undefined, and null
- [ ] Can use `typeof`
- [ ] Understand the `typeof null === "object"` behavior

### Operators

- [ ] Can perform arithmetic
- [ ] Understand `%`
- [ ] Understand `==` vs `===`
- [ ] Understand `!=` vs `!==`

### Variables and Expressions

- [ ] Understand declaration and assignment
- [ ] Know when to use `let`
- [ ] Know when to use `const`
- [ ] Can distinguish expressions from statements

### Arrays

- [ ] Know that indexes start at `0`
- [ ] Can use `push()` and `pop()`
- [ ] Can use `shift()` and `unshift()`
- [ ] Can use `includes()`
- [ ] Can use `join()`
- [ ] Understand `slice()`
- [ ] Understand shared references
- [ ] Understand that `const` doesn't freeze an array
- [ ] Can use array destructuring

### Objects

- [ ] Can create an object
- [ ] Can access properties
- [ ] Can modify properties
- [ ] Can add properties
- [ ] Understand methods
- [ ] Understand `this`
- [ ] Can access nested objects and arrays
- [ ] Understand `Object.freeze()`
- [ ] Understand the difference between `const` and `Object.freeze()`
- [ ] Understand shallow freeze
- [ ] Can use object destructuring

### Functions

- [ ] Can declare a function
- [ ] Can call a function
- [ ] Understand parameters and arguments
- [ ] Understand `return`
- [ ] Know what happens when an argument is missing
- [ ] Understand the purpose of `getMultipleChoices` and its while-loop idea

### Asynchronous JavaScript and APIs

- [ ] Understand what `setTimeout()` does
- [ ] Understand why `fetch()` returns a promise
- [ ] Can use `await` inside an `async` function
- [ ] Can parse a response with `response.json()`
- [ ] Can extract a property with object destructuring
- [ ] Can split a URL with `.split("/")`
- [ ] Understand the indexes in the Dog CEO URL example

### Projects

- [ ] Can connect JavaScript to HTML
- [ ] Can update a page based on a variable
- [ ] Can use a condition to display a result
- [ ] Understand the basic data flow of a quiz
- [ ] Understand how Tic Tac Toe can store board state in an array
- [ ] Can combine DOM selection, functions, async code, API data, and DOM updates
````
