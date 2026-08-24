# JavaScript First Steps

A practical learning guide to JavaScript fundamentals, based on the
**JavaScript First Steps** course material and expanded with the
exercises and notes collected during the training.

The guide starts with the basics of JavaScript and gradually moves into
the DOM, values and data types, operators, expressions, arrays, objects,
functions, methods, and a small quiz project.

------------------------------------------------------------------------

## Table of Contents

1.  [Introduction](#introduction)
2.  [Course Overview](#course-overview)
3.  [What is JavaScript?](#what-is-javascript)
4.  [Where to Write JavaScript](#where-to-write-javascript)
5.  [Section 1 --- DOM](#section-1--dom-document-object-model)
6.  [Section 2 --- Values and Data
    Types](#section-2--values-and-data-types)
7.  [Section 3 --- Operators](#section-3--operators)
8.  [Section 4 --- Expressions and
    Variables](#section-4--expressions-and-variables)
9.  [Section 5 --- Arrays](#section-5--arrays)
10. [Section 6 --- Objects](#section-6--objects)
11. [Section 7 --- Functions](#section-7--functions)
12. [Section 8 --- Quiz Project](#section-8--quiz-project)
13. [Section 9 --- Tic Tac Toe](#section-9--tic-tac-toe)
14. [Quick Reference](#quick-reference)
15. [Practice Checklist](#practice-checklist)
16. [Resources](#resources)

------------------------------------------------------------------------

# Introduction

JavaScript is one of the main technologies used to build interactive
websites.

HTML provides the structure of a page, CSS controls its appearance, and
JavaScript adds behavior and interactivity.

This guide assumes basic knowledge of HTML and CSS. No previous
JavaScript experience is required.

### What you will learn

By the end of this guide, you should understand how to:

-   Run JavaScript in a browser.
-   Use the browser console.
-   Select HTML elements with JavaScript.
-   Read and change page content.
-   Work with strings, numbers, booleans, `undefined`, and `null`.
-   Use arithmetic and comparison operators.
-   Declare and use variables.
-   Understand expressions and statements.
-   Work with arrays and array methods.
-   Understand references and mutability.
-   Create and modify objects.
-   Use object methods and `this`.
-   Work with nested objects.
-   Create and call functions.
-   Understand parameters and arguments.
-   Connect JavaScript logic to the DOM.
-   Build a small interactive quiz.
-   Understand how arrays, objects, functions, and the DOM can work
    together in a project.

------------------------------------------------------------------------

# Course Overview

The learning path follows a gradual progression:

``` text
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
```

The goal is not only to memorize syntax, but to understand how
JavaScript represents data and how that data can be used to control a
web page.

------------------------------------------------------------------------

# What is JavaScript?

JavaScript (JS) is a **high-level, dynamically typed programming
language**.

It is widely used in web browsers to make pages interactive.

JavaScript can:

-   Read HTML elements.
-   Change text and styles.
-   React to user actions.
-   Store and process data.
-   Perform calculations.
-   Work with arrays and objects.
-   Create reusable functions.
-   Communicate with other systems.
-   Run outside the browser through environments such as Node.js.

JavaScript is standardized as **ECMAScript**. The language was created
in 1995 by **Brendan Eich**.

### First JavaScript statement

``` js
console.log("Hello, JavaScript!");
```

`console.log()` prints a value or message to the browser console.

------------------------------------------------------------------------

# Where to Write JavaScript

There are three common ways to run JavaScript.

## 1. Browser DevTools Console

The console is useful for quick experiments.

Open a web page and:

``` text
Right-click → Inspect → Console
```

Then try:

``` js
console.log("Hello!");
```

The console is especially useful while learning because you can
immediately see the result of an expression.

------------------------------------------------------------------------

## 2. Inline JavaScript

JavaScript can be written directly inside an HTML `<script>` element.

``` html
<script>
  console.log("Hello from inline JavaScript");
</script>
```

This is useful for simple examples, but larger projects are easier to
maintain when JavaScript is separated from HTML.

------------------------------------------------------------------------

## 3. External JavaScript File

A JavaScript file can be connected to an HTML page.

``` html
<script src="app.js"></script>
```

Then `app.js` can contain:

``` js
console.log("Hello from app.js");
```

### Recommended structure

``` text
project/
├── index.html
├── style.css
└── app.js
```

Keeping HTML, CSS, and JavaScript separated makes projects easier to
organize and maintain.

------------------------------------------------------------------------

# Section 1 --- DOM (Document Object Model)

## What is the DOM?

The **Document Object Model (DOM)** is a tree-like representation of an
HTML document.

The browser turns HTML elements into objects/nodes that JavaScript can
access and manipulate.

For example:

``` text
document
└── html
    ├── head
    └── body
        ├── h1
        └── p
```

JavaScript can use the DOM to:

-   Find elements.
-   Read their content.
-   Change their content.
-   Change styles.
-   Add or remove classes.
-   Respond to user events.

------------------------------------------------------------------------

## Selecting Elements

### `querySelector()`

Selects the first element that matches a CSS selector.

``` js
const title = document.querySelector("h1");
```

It can also use IDs and classes:

``` js
document.querySelector("#title");
document.querySelector(".card");
```

------------------------------------------------------------------------

### `querySelectorAll()`

Selects all elements that match a CSS selector.

``` js
const paragraphs = document.querySelectorAll("p");
```

The result is a `NodeList`.

------------------------------------------------------------------------

### `getElementById()`

Selects an element using its ID.

``` js
const title = document.getElementById("title");
```

------------------------------------------------------------------------

### `getElementsByTagName()`

Selects elements by tag name.

``` js
const items = document.getElementsByTagName("li");
```

------------------------------------------------------------------------

### `getElementsByClassName()`

Selects elements by class name.

``` js
const cards = document.getElementsByClassName("card");
```

------------------------------------------------------------------------

## `.length`

`.length` can be used to find how many elements were returned by many
DOM collection methods.

``` js
const items = document.querySelectorAll("li");

console.log(items.length);
```

------------------------------------------------------------------------

## `.textContent`

`.textContent` reads or changes the text inside an element.

Read text:

``` js
const title = document.querySelector("h1");

console.log(title.textContent);
```

Change text:

``` js
title.textContent = "New Title";
```

------------------------------------------------------------------------

## Changing a Web Page

JavaScript can modify an element after selecting it.

``` js
const title = document.querySelector("h1");

title.textContent = "New Title";
title.style.color = "blue";
title.classList.add("highlight");
```

------------------------------------------------------------------------

## Events

JavaScript can react to user actions such as clicks.

``` js
const button = document.querySelector("#submit-btn");

button.addEventListener("click", function () {
  button.textContent = "Submitted!";
});
```

The general pattern is:

``` js
element.addEventListener("event", function () {
  // code to run
});
```

Common events include:

``` text
click
input
change
submit
mouseover
keydown
```

------------------------------------------------------------------------

## DOM Exercise

**Task:** Select every `<li>` on the page and print the number of items.

``` js
const items = document.querySelectorAll("li");

console.log(items.length);
```

------------------------------------------------------------------------

## DOM Refresh Behavior

DOM changes made by JavaScript normally affect the current page in
memory.

For example:

``` js
document.body.style.backgroundColor = "black";
```

If the page is refreshed, the browser loads the original HTML and CSS
again, so a temporary JavaScript DOM change is normally lost unless the
application stores the change somewhere persistent.

------------------------------------------------------------------------

# Section 2 --- Values and Data Types

JavaScript works with different kinds of values.

Important primitive data types introduced in this course include:

  Type        Example
  ----------- -----------------
  String      `"hello"`
  Number      `42`, `3.14`
  Boolean     `true`, `false`
  Undefined   `undefined`
  Null        `null`

------------------------------------------------------------------------

## `typeof`

The `typeof` operator can be used to inspect the type of a value.

``` js
typeof "hello";     // "string"
typeof 42;          // "number"
typeof true;        // "boolean"
typeof undefined;   // "undefined"
```

A well-known JavaScript behavior is:

``` js
typeof null;        // "object"
```

This is a historical JavaScript quirk.

Arrays and ordinary objects also report:

``` js
typeof [1, 2, 3];   // "object"
typeof {};          // "object"
```

------------------------------------------------------------------------

## Strings

A string represents text.

JavaScript supports:

``` js
"double quotes"
'single quotes'
`template literals`
```

Example:

``` js
const greeting = "Hello";

console.log(greeting.length);
console.log(greeting[0]);
```

Output:

``` text
5
H
```

String indexes start at `0`.

``` text
H e l l o
0 1 2 3 4
```

------------------------------------------------------------------------

## Useful String Methods

### `.length`

``` js
const name = "Shahd";

console.log(name.length);
```

### `.indexOf()`

Returns the position of a matching substring.

``` js
const phrase = "JavaScript is fun";

phrase.indexOf("is");
```

### `.includes()`

Checks whether a string contains another string.

``` js
phrase.includes("fun"); // true
```

### `.startsWith()`

Checks whether a string starts with a particular value.

``` js
phrase.startsWith("Java"); // true
```

### `.toLowerCase()`

Converts the string to lowercase.

``` js
phrase.toLowerCase();
```

------------------------------------------------------------------------

## String Exercise

Given:

``` js
const name = "Shahd";
```

Print the length and check whether the name includes `"a"`.

``` js
console.log(name.length);
console.log(name.includes("a"));
```

------------------------------------------------------------------------

# Section 3 --- Operators

Operators allow JavaScript to perform calculations and comparisons.

## Arithmetic Operators

``` js
5 + 3;    // 8
5 - 3;    // 2
5 * 3;    // 15
5 / 3;    // 1.666...
5 % 3;    // 2
2 ** 3;   // 8
```

  Operator   Meaning
  ---------- --------------------
  `+`        Addition
  `-`        Subtraction
  `*`        Multiplication
  `/`        Division
  `%`        Remainder / modulo
  `**`       Exponentiation

------------------------------------------------------------------------

## Operator Exercise

Calculate the area of a rectangle.

``` js
const width = 4;
const height = 7;

const area = width * height;

console.log(area);
```

Result:

``` text
28
```

------------------------------------------------------------------------

## Comparison Operators

Comparison operators produce a boolean result.

``` js
5 > 3;     // true
5 < 3;     // false
5 >= 5;    // true
5 <= 4;    // false
```

------------------------------------------------------------------------

## Equality

JavaScript provides loose and strict equality.

### Loose equality

``` js
5 == "5"; // true
```

Loose equality can convert types before comparing.

### Strict equality

``` js
5 === "5"; // false
```

Strict equality checks both value and type.

### Strict inequality

``` js
5 !== "5"; // true
```

### Best Practice

Prefer:

``` js
===
!==
```

over:

``` js
==
!=
```

because strict comparisons reduce unexpected type conversion.

------------------------------------------------------------------------

# Section 4 --- Expressions and Variables

## What is an Expression?

An **expression** is a piece of code that produces a value.

Examples:

``` js
3 + 4;
```

produces:

``` text
7
```

Another example:

``` js
"a" + "b";
```

produces:

``` text
"ab"
```

Comparison expressions also produce values:

``` js
age > 18;
```

produces either:

``` text
true
```

or:

``` text
false
```

------------------------------------------------------------------------

## Declaring and Assigning Variables

A variable can be declared first and assigned later:

``` js
let age;

age = 20;
```

Or both can happen together:

``` js
let name = "Ali";
```

------------------------------------------------------------------------

## `let`

`let` allows a variable to be reassigned.

``` js
let age = 20;

age = 21;
```

------------------------------------------------------------------------

## `const`

`const` requires an initial value and prevents reassignment of the
variable.

``` js
const pi = 3.14159;
```

This is not allowed:

``` js
const pi = 3.14159;

pi = 4; // TypeError
```

------------------------------------------------------------------------

## Variables Exercise

``` js
let favoriteColor = "teal";

console.log(favoriteColor);
```

------------------------------------------------------------------------

## What are Variables?

Variables are named references used to store or access values so the
values can be reused in a program.

``` js
const score = 8;

console.log(score);
```

The name `score` gives the program a way to refer to the value.

------------------------------------------------------------------------

## Evaluating Code

JavaScript evaluates nested expressions so that inner operations can
contribute to the final result.

``` js
const result = (2 + 3) * (4 - 1);
```

Conceptually:

``` text
(2 + 3) * (4 - 1)
     ↓       ↓
     5   *   3
         ↓
        15
```

------------------------------------------------------------------------

## Statements vs Expressions

### Expression

Produces a value:

``` js
3 + 4;
```

``` js
age > 18;
```

### Statement

Performs an action or controls execution.

``` js
if (age > 18) {
  console.log("adult");
}
```

The `if` structure is a statement, while:

``` js
age > 18
```

is an expression inside it.

------------------------------------------------------------------------

# Section 5 --- Arrays

## What is an Array?

An array is an ordered collection of values.

Indexes start at `0`.

``` js
const fruits = ["apple", "banana", "cherry"];

console.log(fruits[0]);
console.log(fruits.length);
```

Output:

``` text
apple
3
```

Array indexes:

``` text
apple   banana   cherry
  0       1        2
```

------------------------------------------------------------------------

## Useful Array Methods

``` js
const nums = [1, 2, 3];
```

### `push()`

Adds an item to the end.

``` js
nums.push(4);
```

Result:

``` js
[1, 2, 3, 4]
```

### `pop()`

Removes the last item.

``` js
nums.pop();
```

### `unshift()`

Adds an item to the beginning.

``` js
nums.unshift(0);
```

### `shift()`

Removes the first item.

``` js
nums.shift();
```

### `includes()`

Checks whether an array contains a value.

``` js
nums.includes(2);
```

### `join()`

Combines array elements into a string.

``` js
nums.join("-");
```

Example:

``` text
"1-2-3"
```

### `slice()`

Returns part of an array without changing the original array.

``` js
nums.slice(0, 2);
```

Result:

``` js
[1, 2]
```

------------------------------------------------------------------------

## Array Mutability and `const`

A very important concept:

> `const` prevents reassignment of the variable, but it does not make
> the contents of an array immutable.

This is allowed:

``` js
const colors = ["red", "green"];

colors.push("blue");

console.log(colors);
```

Result:

``` js
["red", "green", "blue"]
```

But this is not allowed:

``` js
colors = ["yellow"];
```

because the variable itself cannot be reassigned.

### Key idea

``` text
const
  ↓
protects the reference
  ↓
does not automatically freeze the array contents
```

------------------------------------------------------------------------

## Array Example

``` js
const operands = [4, 6];

const sum = operands[0] + operands[1];

console.log(sum); // 10

operands[0] = 5;

const newSum = operands[0] + operands[1];

console.log(newSum); // 11
```

The array can still be modified even though it was declared with
`const`.

------------------------------------------------------------------------

## Shared References

Consider:

``` js
let array1 = [1, 2, 3];

let array2 = array1;
```

`array2` does not create an independent copy of the array.

Both variables refer to the same array.

``` js
array1[1] = 4;

console.log(array1);
console.log(array2);
```

Both show:

``` js
[1, 4, 3]
```

### Visual model

``` text
array1 ───────┐
              ↓
          [1, 4, 3]
              ↑
array2 ───────┘
```

------------------------------------------------------------------------

## Mutable and Immutable Data

Understanding mutability helps reduce unexpected changes.

Immutable data is useful because it can:

-   Reduce unexpected changes.
-   Make code easier to reason about.
-   Reduce the likelihood of bugs.
-   Make program behavior more predictable.

------------------------------------------------------------------------

# Section 6 --- Objects

## What is an Object?

Objects group related values together using **properties**.

Example:

``` js
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

``` text
name → "JavaScript"
abbreviation → "JS"
birthYear → 1995
```

------------------------------------------------------------------------

## Accessing Object Properties

Dot notation:

``` js
console.log(js.name);
```

Output:

``` text
JavaScript
```

Another example:

``` js
js.birthYear;
```

------------------------------------------------------------------------

## Modifying and Adding Properties

Existing properties can be changed:

``` js
indecisive.lunch = "tacos";
```

New properties can be added:

``` js
indecisive.snack = "chips";
```

Example:

``` js
const indecisive = {
  lunch: "sandwich"
};

indecisive.lunch = "tacos";
indecisive.snack = "chips";
```

------------------------------------------------------------------------

## Objects and Arrays

Arrays are objects in JavaScript.

``` js
typeof { snack: "chips" };
// "object"

typeof ["chips"];
// "object"
```

This does not mean arrays and ordinary objects behave identically.
Arrays have special behavior and methods designed for ordered
collections.

------------------------------------------------------------------------

## Objects Exercise

Create an object representing a person.

``` js
const anjana = {
  name: "Anjana",
  home: "San Francisco",
  languages: ["English", "German", "French"],
  pet: null,
  vehicle: "Vespa",
  hobbies: ["travel", "climbing", "gaming", "lindy hop"]
};
```

You can access nested array values:

``` js
anjana.languages[0];
anjana.hobbies[2];
```

------------------------------------------------------------------------

# Object Methods

A function stored as an object property is called a **method**.

``` js
const dog = {
  name: "Ein",
  breed: "Corgi",

  speak: function () {
    console.log("woof woof");
  }
};
```

Call the method:

``` js
dog.speak();
```

Output:

``` text
woof woof
```

------------------------------------------------------------------------

## The `this` Keyword

Inside an object method, `this` can refer back to the object on which
the method is called.

``` js
anjana.speak = function () {
  console.log("Hi my name is", this.name);
};

anjana.speak();
```

Output:

``` text
Hi my name is Anjana
```

Here:

``` js
this.name
```

refers to the `name` property of the object used to call the method.

------------------------------------------------------------------------

## Object Methods Exercise

Add a `greet` method to the `dog` object.

``` js
dog.greet = function () {
  console.log("Hi, I'm " + this.name + "!");
};

dog.greet();
```

Output:

``` text
Hi, I'm Ein!
```

------------------------------------------------------------------------

# Built-In Objects

JavaScript provides built-in objects and utilities.

## `Math`

``` js
Math.max(3, 7, 2);
// 7

Math.round(4.6);
// 5
```

------------------------------------------------------------------------

## `Date`

``` js
const now = new Date();

console.log(now);
```

------------------------------------------------------------------------

## `JSON`

Objects can be converted to JSON strings.

``` js
JSON.stringify({ a: 1 });
```

Result:

``` text
'{"a":1}'
```

------------------------------------------------------------------------

## `Object.freeze()`

`Object.freeze()` prevents changes to an object.

``` js
const user = {
  name: "Ali"
};

Object.freeze(user);
```

After freezing, the object cannot normally have its properties added,
changed, or deleted.

``` text
Object.freeze()
      ↓
prevents property changes
prevents adding properties
prevents deleting properties
```

------------------------------------------------------------------------

## Console Methods

### `console.log()`

``` js
console.log("Hello");
```

Used for normal console output.

### `console.warn()`

``` js
console.warn("Something may be wrong");
```

Used for warning messages.

------------------------------------------------------------------------

# Strings as Primitive Values

Strings are primitive values.

JavaScript allows string methods such as:

``` js
const text = "JavaScript";

text.length;
text.indexOf("Script");
```

JavaScript temporarily provides string-object behavior so methods can be
used on the primitive string.

The original string value remains immutable.

For example:

``` js
const word = "hello";

word.toUpperCase();

console.log(word);
```

The original `word` value is not changed automatically.

------------------------------------------------------------------------

# Nested Objects

Objects can contain other objects.

``` js
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
```

Accessing nested properties:

``` js
const tiramisu = menu.lunch.dessert;

console.log(tiramisu);
```

Result:

``` text
tiramisu
```

------------------------------------------------------------------------

## Nested Arrays and Objects

An object can contain arrays, and arrays can contain objects.

Example:

``` js
const spiceGirls = {
  motto: "Girl Power",

  members: [
    { name: "Mel B", nickname: "Scary" },
    { name: "Geri", nickname: "Ginger" },
    { name: "Mel C", nickname: "Sporty" },
    { name: "Emma", nickname: "Baby" },
    { name: "Victoria", nickname: "Posh" }
  ],

  albums: ["Spice", "Spiceworld"]
};
```

Examples:

``` js
spiceGirls.motto;
```

``` js
spiceGirls.members[1];
```

``` js
spiceGirls.albums[1];
```

``` js
spiceGirls.members[4].name;
```

The last expression accesses:

``` text
object
  ↓
members array
  ↓
index 4
  ↓
name property
```

------------------------------------------------------------------------

# Section 7 --- Functions

Functions allow us to group reusable instructions.

## Basic Function

``` js
function greet() {
  console.log("Hello!");
}
```

Call the function:

``` js
greet();
```

------------------------------------------------------------------------

## Parameters and Arguments

A function can receive information through parameters.

``` js
function greet(name) {
  console.log("Hello " + name);
}
```

Calling the function:

``` js
greet("Reem");
```

Here:

-   `name` is the **parameter**.
-   `"Reem"` is the **argument**.

------------------------------------------------------------------------

## Multiple Parameters

``` js
function add(a, b) {
  return a + b;
}

const result = add(3, 4);

console.log(result);
```

Result:

``` text
7
```

------------------------------------------------------------------------

## Fewer Arguments

JavaScript allows a function to be called with fewer arguments than the
number of declared parameters.

For example:

``` js
function add(a, b) {
  return a + b;
}

add(5);
```

The missing parameter receives:

``` js
undefined
```

Therefore the result involves `undefined`:

``` js
5 + undefined
```

which produces:

``` text
NaN
```

This is important when understanding how JavaScript handles function
arguments.

------------------------------------------------------------------------

## Function Returning a Value

``` js
function square(number) {
  return number * number;
}

const result = square(5);

console.log(result);
```

Result:

``` text
25
```

------------------------------------------------------------------------

# Section 8 --- Quiz Project

The quiz project brings several concepts together.

It uses:

-   Variables.
-   Data types.
-   Operators.
-   Conditional logic.
-   Functions.
-   DOM selection.
-   DOM updates.
-   User input.

------------------------------------------------------------------------

## Project Setup

A simple project can contain:

``` text
quiz-project/
├── index.html
├── style.css
└── script.js
```

HTML:

``` html
<p id="result"></p>
<p id="message"></p>

<script src="script.js"></script>
```

JavaScript:

``` js
const result = document.querySelector("#result");
const score = 8;

result.textContent = "Your score: " + score;
```

------------------------------------------------------------------------

## Variables in the Quiz

``` js
let userAnswer = "B";
```

The variable stores the selected answer.

------------------------------------------------------------------------

## Conditional Result

``` js
const message = document.querySelector("#message");

if (score >= 5) {
  message.textContent = "You passed!";
} else {
  message.textContent = "Try again!";
}
```

This demonstrates how JavaScript can combine:

``` text
Variable
   ↓
Condition
   ↓
Decision
   ↓
DOM update
```

------------------------------------------------------------------------

## `getMultipleChoices`

A quiz application can use a function such as `getMultipleChoices` to
obtain or process the multiple-choice options used by the quiz.

The important concept is that functions allow repeated quiz logic to be
organized into reusable blocks rather than writing the same code
repeatedly.

------------------------------------------------------------------------

# Section 9 --- Tic Tac Toe

Tic Tac Toe demonstrates how several JavaScript concepts can work
together:

-   Arrays.
-   Objects/functions when needed.
-   Events.
-   DOM manipulation.
-   User interaction.
-   Updating application state.

A simple board can be represented by an array:

``` js
const board = [
  "", "", "",
  "", "", "",
  "", "", ""
];
```

The center square is index `4`.

``` js
board[4] = "X";
```

The data now represents:

``` text
|   |   |   |
|---|---|---|
|   | X |   |
|---|---|---|
|   |   |   |
```

------------------------------------------------------------------------

## Data and UI

A useful way to understand the Tic Tac Toe example is:

``` text
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

The array represents the application data, while the DOM represents what
the user sees.

------------------------------------------------------------------------

# JavaScript + DOM Mental Model

The most important idea in the course is the relationship between
**data, logic, and the page**.

``` text
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

------------------------------------------------------------------------

# Quick Reference

## DOM

``` js
document.querySelector("h1");
document.querySelectorAll("p");
document.getElementById("title");
document.getElementsByTagName("li");
document.getElementsByClassName("card");
```

## DOM Content

``` js
element.textContent;
element.textContent = "New text";
```

## Events

``` js
element.addEventListener("click", function () {
  // action
});
```

## Data Types

``` js
typeof "text";
typeof 42;
typeof true;
typeof undefined;
typeof null;
```

## Strings

``` js
text.length;
text[0];
text.indexOf("x");
text.includes("x");
text.startsWith("x");
text.toLowerCase();
```

## Operators

``` js
+  -  *  /  %  **
>  <  >=  <=
=== !==
```

## Variables

``` js
let age = 20;
const name = "Ali";
```

## Arrays

``` js
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

## Objects

``` js
object.property;
object.property = value;
object.newProperty = value;
```

## Methods

``` js
object.method();
```

## `this`

``` js
const user = {
  name: "Ali",

  greet: function () {
    console.log(this.name);
  }
};
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## 1. Forgetting that array indexes start at 0

``` js
const fruits = ["apple", "banana", "cherry"];

fruits[0]; // apple
fruits[1]; // banana
fruits[2]; // cherry
```

------------------------------------------------------------------------

## 2. Confusing `=` with `===`

``` js
=
```

is used for assignment.

``` js
===
```

is used for strict equality comparison.

------------------------------------------------------------------------

## 3. Thinking `const` makes an array immutable

This is allowed:

``` js
const numbers = [1, 2];

numbers.push(3);
```

But this is not:

``` js
numbers = [4, 5];
```

------------------------------------------------------------------------

## 4. Forgetting that objects and arrays are reference values

``` js
let a = [1, 2, 3];
let b = a;

b[0] = 99;

console.log(a);
```

`a` is also changed because both variables refer to the same array.

------------------------------------------------------------------------

## 5. Selecting an element that does not exist

``` js
const button = document.querySelector("#submit-btn");
```

If the page does not contain that element, `button` can be `null`.

Always make sure the selector matches an existing HTML element.

------------------------------------------------------------------------

# Practice Checklist

Use this checklist to review the course.

### JavaScript Basics

-   [ ] I can explain what JavaScript is.
-   [ ] I can run JavaScript in the browser console.
-   [ ] I know how to connect an external `.js` file.

### DOM

-   [ ] I can use `querySelector()`.
-   [ ] I can use `querySelectorAll()`.
-   [ ] I can use `getElementById()`.
-   [ ] I understand `.length`.
-   [ ] I can read and change `.textContent`.
-   [ ] I can respond to a click with `addEventListener()`.

### Data Types

-   [ ] I know string, number, boolean, undefined, and null.
-   [ ] I can use `typeof`.
-   [ ] I understand the `typeof null === "object"` behavior.

### Operators

-   [ ] I can perform arithmetic.
-   [ ] I understand `%`.
-   [ ] I understand `==` vs `===`.
-   [ ] I understand `!=` vs `!==`.

### Variables and Expressions

-   [ ] I understand declaration and assignment.
-   [ ] I know when to use `let`.
-   [ ] I know when to use `const`.
-   [ ] I can distinguish expressions from statements.

### Arrays

-   [ ] I know that indexes start at 0.
-   [ ] I can use `push()` and `pop()`.
-   [ ] I can use `shift()` and `unshift()`.
-   [ ] I can use `includes()`.
-   [ ] I can use `join()`.
-   [ ] I understand `slice()`.
-   [ ] I understand shared references.
-   [ ] I understand that `const` does not freeze an array.

### Objects

-   [ ] I can create an object.
-   [ ] I can access properties.
-   [ ] I can modify properties.
-   [ ] I can add properties.
-   [ ] I understand methods.
-   [ ] I understand `this`.
-   [ ] I can access nested objects and arrays.
-   [ ] I understand `Object.freeze()`.

### Functions

-   [ ] I can declare a function.
-   [ ] I can call a function.
-   [ ] I understand parameters and arguments.
-   [ ] I understand `return`.
-   [ ] I know what happens when an argument is missing.

### Projects

-   [ ] I can connect JavaScript to HTML.
-   [ ] I can update a page based on a variable.
-   [ ] I can use a condition to display a result.
-   [ ] I understand the basic data flow of a quiz.
-   [ ] I understand how Tic Tac Toe can store board state in an array.

------------------------------------------------------------------------

# Final Summary

  -----------------------------------------------------------------------
  Section                             Main Idea
  ----------------------------------- -----------------------------------
  Getting Started                     JavaScript adds behavior and
                                      interactivity to web pages

  DOM                                 JavaScript can read and change HTML
                                      elements

  Values & Data Types                 JavaScript works with different
                                      types of values

  Strings                             Text values provide useful
                                      properties and methods

  Operators                           Operators perform calculations and
                                      comparisons

  Expressions                         Expressions produce values

  Variables                           Variables provide named references
                                      to values

  Arrays                              Arrays store ordered collections of
                                      values

  Mutability                          `const` protects reassignment, not
                                      the contents of arrays/objects

  Objects                             Objects group related data through
                                      properties

  Methods                             Functions stored on objects are
                                      methods

  `this`                              `this` can refer to the object used
                                      to call a method

  Functions                           Functions organize reusable logic

  Quiz Project                        Combines variables, logic,
                                      functions, and DOM manipulation

  Tic Tac Toe                         Demonstrates state, events, arrays,
                                      and DOM updates
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Resources

-   **JavaScript First Steps Course:**
    https://anjana.dev/javascript-first-steps/
-   **Tic Tac Toe Course Demo:**
    https://anjana.dev/javascript-first-steps/1-tictactoe.html
-   **MDN Web Docs:** https://developer.mozilla.org/en-US/

------------------------------------------------------------------------

## Notes

This README keeps the original course topics and examples while
expanding the structure into a more complete study reference. The
additional organization and explanations are intended to make the
material easier to review and use as a GitHub learning resource.
