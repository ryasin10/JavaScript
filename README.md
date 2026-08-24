# JavaScript First Steps

A practical introduction to JavaScript covering the fundamentals needed to build interactive web pages.

This README is organized as a learning guide and includes JavaScript basics, DOM manipulation, values and data types, operators, expressions, arrays, objects, functions, and a small quiz project.

---

# Table of Contents

1. [Introduction](#introduction)
2. [Course Overview](#course-overview)
3. [What is JavaScript?](#what-is-javascript)
4. [Where to Write JavaScript](#where-to-write-javascript)
5. [Section 1 — DOM](#section-1--dom-document-object-model)
6. [Section 2 — Values and Data Types](#section-2--values-and-data-types)
7. [Section 3 — Operators](#section-3--operators)
8. [Section 4 — Expressions and Variables](#section-4--expressions-and-variables)
9. [Section 5 — Arrays](#section-5--arrays)
10. [Section 6 — Objects](#section-6--objects)
11. [Section 7 — Functions](#section-7--functions)
12. [Section 8 — Quiz Project](#section-8--quiz-project)
13. [Tic-Tac-Toe Project](#tic-tac-toe-project)
14. [Quick Review](#quick-review)
15. [Useful Resources](#useful-resources)

---

# Introduction

JavaScript is one of the main technologies used to create interactive websites.

HTML provides the structure of a webpage, CSS controls its appearance, and JavaScript adds behavior and interaction.

Examples of things JavaScript can do:

- Change text on a webpage
- Change styles
- Respond to button clicks
- Read user input
- Work with arrays and objects
- Perform calculations
- Update the DOM
- Build interactive applications

This course starts with the basic concepts and gradually combines them into small practical projects.

---

# Course Overview

The course follows this learning path:

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
DOM + JavaScript
       ↓
Quiz Project
       ↓
Tic-Tac-Toe

The goal is not only to understand JavaScript syntax, but also to understand how JavaScript works with webpage elements and data.

What is JavaScript?

JavaScript (JS) is a high-level, dynamically typed programming language.

It is widely used in web browsers to make websites interactive.

JavaScript can also run outside the browser using environments such as Node.js.

JavaScript is standardized by ECMAScript.

JavaScript was created in 1995 by Brendan Eich.

A simple JavaScript program:

console.log("Hello, JavaScript!");

The console.log() method prints information to the browser console.

Where to Write JavaScript

There are three common ways to write JavaScript.

1. Browser DevTools Console

The browser console is useful for testing small pieces of JavaScript.

Open:

Right Click → Inspect → Console

Example:

console.log("Hello!");
2. Inline JavaScript

JavaScript can be written directly inside an HTML <script> element.

<script>
  console.log("Hello from inline JavaScript");
</script>
3. External JavaScript File

For real projects, JavaScript is usually placed in a separate file.

HTML:

<script src="app.js"></script>

JavaScript:

console.log("Hello from app.js");

Keeping JavaScript in an external file makes projects easier to organize and maintain.

Section 1 — DOM (Document Object Model)
What is the DOM?

The Document Object Model (DOM) is a tree-like representation of an HTML document.

The browser converts the HTML page into objects that JavaScript can access and manipulate.

Example:

document
 └── html
      ├── head
      └── body
           ├── h1
           ├── p
           └── button

JavaScript can use the DOM to:

Find HTML elements
Read their content
Change their content
Change styles
Add or remove classes
Respond to user events
The document Object

The document object represents the current HTML document.

For example:

document.title;

This returns the title of the current webpage.

The title can also be changed:

document.title = "My JavaScript Page";

The page body can be accessed using:

document.body;
Finding Elements in the DOM

There are several methods for selecting HTML elements.

getElementById()

Selects one element using its id.

HTML:

<h1 id="title">Hello</h1>

JavaScript:

const title = document.getElementById("title");
querySelector()

Returns the first element that matches a CSS selector.

const title = document.querySelector("h1");

Using an ID:

const title = document.querySelector("#title");

Using a class:

const box = document.querySelector(".box");
querySelectorAll()

Selects all elements matching a CSS selector.

const paragraphs = document.querySelectorAll("p");

The result is a NodeList.

getElementsByTagName()

Selects elements using their HTML tag name.

const paragraphs = document.getElementsByTagName("p");

For example:

const items = document.getElementsByTagName("li");

console.log(items.length);
getElementsByClassName()

Selects elements that have a specific class.

const boxes = document.getElementsByClassName("box");

The number of matching elements can be checked using:

console.log(boxes.length);
.length

The .length property tells us how many items are contained in a collection.

Example:

const items = document.querySelectorAll("li");

console.log(items.length);

If there are five <li> elements, the result will be:

5
.textContent

The .textContent property can be used to read or change the text inside an element.

HTML:

<h1 id="title">Hello</h1>

Read the text:

const title = document.querySelector("#title");

console.log(title.textContent);

Change the text:

title.textContent = "New Title";
Changing a Web Page

JavaScript can modify the webpage after it has loaded.

Example:

const title = document.querySelector("h1");

title.textContent = "New Title";
title.style.color = "blue";
title.classList.add("highlight");

JavaScript changed:

The text
The style
The CSS class
Handling Events

JavaScript can respond to user actions.

For example, a button click:

const button = document.querySelector("#submit-btn");

button.addEventListener("click", function () {
  button.textContent = "Submitted!";
});

The addEventListener() method waits for an event and executes a function when that event occurs.

DOM Changes and Page Refresh

DOM changes made using JavaScript normally exist only in the current page session.

For example:

document.querySelector("h1").textContent = "Changed!";

If the page is refreshed, the browser loads the original HTML again.

Therefore:

JavaScript DOM change
        ↓
Current page changes
        ↓
Refresh page
        ↓
Original HTML is loaded again

To permanently save data, JavaScript would need to use mechanisms such as:

Local Storage
Databases
Server-side storage
Files
DOM Exercise
Task

Select every <li> element and print how many elements were found.

const items = document.querySelectorAll("li");

console.log(items.length);
Section 2 — Values and Data Types

JavaScript works with different types of values.

The basic primitive data types include:

Type	Example
String	"hello"
Number	42, 3.14
Boolean	true, false
Undefined	undefined
Null	null
typeof

The typeof operator can be used to check the type of a value.

typeof "hello";
// "string"

typeof 42;
// "number"

typeof true;
// "boolean"

typeof undefined;
// "undefined"

A famous JavaScript behavior is:

typeof null;
// "object"

Although null represents an intentional absence of a value, JavaScript reports its type as "object" because of a historical language behavior.

Strings

A string represents text.

Strings can use:

"double quotes"
'single quotes'
`template literals`

Example:

const greeting = "Hello";
String Length

The .length property returns the number of characters.

const greeting = "Hello";

console.log(greeting.length);

Output:

5
String Indexing

Characters can be accessed using indexes.

JavaScript indexes start from 0.

const greeting = "Hello";

console.log(greeting[0]);
// H

console.log(greeting[1]);
// e

Visual representation:

H   e   l   l   o
0   1   2   3   4
Useful String Methods
indexOf()

Finds the position of a substring.

const phrase = "JavaScript is fun";

console.log(phrase.indexOf("is"));
includes()

Checks whether a string contains another string.

phrase.includes("fun");
// true
startsWith()

Checks whether a string starts with a specific value.

phrase.startsWith("Java");
// true
toLowerCase()

Converts the string to lowercase.

phrase.toLowerCase();
// "javascript is fun"
String Exercise

Given:

const name = "Shahd";

Print the length and check whether it contains "a".

console.log(name.length);
console.log(name.includes("a"));

Output:

5
true
Section 3 — Operators

Operators are symbols used to perform operations on values.

Arithmetic Operators
5 + 3;   // 8
5 - 3;   // 2
5 * 3;   // 15
5 / 3;   // 1.666...
5 % 3;   // 2
2 ** 3;  // 8
Operator	Meaning
+	Addition
-	Subtraction
*	Multiplication
/	Division
%	Remainder
**	Exponentiation
Modulo %

The % operator returns the remainder after division.

10 % 3;
// 1

Because:

10 ÷ 3 = 3 remainder 1

Modulo is useful for checking whether numbers are even or odd.

10 % 2 === 0;
// true
Comparison Operators
5 > 3;    // true
5 < 3;    // false
5 >= 5;   // true
5 <= 4;   // false

Common comparison operators:

Operator	Meaning
>	Greater than
<	Less than
>=	Greater than or equal
<=	Less than or equal
===	Strict equality
!==	Strict inequality
Equality: == vs ===

JavaScript has two common equality operators.

Loose Equality
5 == "5";
// true

JavaScript converts the values before comparing them.

Strict Equality
5 === "5";
// false

The values have different types.

Best practice:

=== 
!==

are generally preferred because they avoid unexpected type conversion.

Section 4 — Expressions and Variables
What is an Expression?

An expression is a piece of code that produces a value.

Examples:

3 + 4;

produces:

7

Another example:

"a" + "b";

produces:

"ab"
Variables

Variables allow us to store and reuse values.

JavaScript commonly uses:

let
const
let

A variable declared using let can be reassigned.

let age = 20;

age = 21;
const

A variable declared using const cannot be reassigned.

const pi = 3.14159;

This is not allowed:

pi = 4;

It produces an error because the variable cannot be reassigned.

Declaration and Assignment

Declaration:

let age;

Assignment:

age = 20;

Both can be combined:

let name = "Ali";
Variables as References

Variables can be thought of as named references to values.

const name = "Ali";

console.log(name);

Instead of writing "Ali" repeatedly, we can use the variable:

console.log(name);
Evaluating Expressions

JavaScript evaluates nested expressions from the inside outward.

Example:

const result = (2 + 3) * (4 - 1);

First:

2 + 3 = 5

Then:

4 - 1 = 3

Finally:

5 * 3 = 15

Result:

15
Statements vs Expressions
Expression

Produces a value:

3 + 4

or:

age > 18
Statement

Performs an action or controls program flow.

Example:

if (age > 18) {
  console.log("Adult");
}

The if statement controls what the program does.

Variables Exercise

Create a variable for your favorite color and print it.

let favoriteColor = "teal";

console.log(favoriteColor);
Section 5 — Arrays

An array is an ordered collection of values.

Example:

const fruits = ["apple", "banana", "cherry"];

Arrays use zero-based indexing.

fruits[0];
// "apple"

fruits[1];
// "banana"

fruits.length;
// 3
Array Indexing
apple     banana     cherry
  0          1          2

The first element always has index 0.

Array Methods
push()

Adds an item to the end.

const nums = [1, 2, 3];

nums.push(4);

console.log(nums);
// [1, 2, 3, 4]
pop()

Removes the last item.

nums.pop();
unshift()

Adds an item to the beginning.

nums.unshift(0);
shift()

Removes the first item.

nums.shift();
includes()

Checks whether an item exists.

nums.includes(2);
// true
join()

Combines array elements into a string.

nums.join("-");

Example:

1-2-3
slice()

Returns part of an array without changing the original array.

const nums = [1, 2, 3];

const result = nums.slice(0, 2);

console.log(result);
// [1, 2]
const and Arrays

A very important JavaScript concept:

const prevents reassignment of the variable, but it does not make the array contents immutable.

Example:

const operands = [4, 6];

operands[0] = 5;

This is allowed.

The array becomes:

[5, 6]

But this is not allowed:

operands = [10, 20];

because the variable itself cannot be reassigned.

const Fixes the Reference

Think of it as:

const operands
      ↓
   [4, 6]

The reference cannot be changed to another array.

However, the contents of the array can still be changed.

operands[0] = 5;
Array Example
const operands = [4, 6];

const sum = operands[0] + operands[1];

console.log(sum);
// 10

operands[0] = 5;

const newSum = operands[0] + operands[1];

console.log(newSum);
// 11
Mutable vs Immutable Data

Mutable data can be changed after it is created.

Arrays are mutable.

const colors = ["red", "green"];

colors.push("blue");

console.log(colors);
// ["red", "green", "blue"]

However:

colors = ["yellow"];

is not allowed because colors was declared with const.

Shared Array References

Consider:

let array1 = [1, 2, 3];

let array2 = array1;

Both variables reference the same array.

array1 ─────┐
            ↓
        [1, 2, 3]
            ↑
array2 ─────┘

Changing the array through one variable also affects the other.

array1[1] = 4;

console.log(array1);
// [1, 4, 3]

console.log(array2);
// [1, 4, 3]

This is an important concept when working with JavaScript objects and arrays.

Section 6 — Objects

Objects are used to group related data together.

An object contains properties.

Example:

const js = {
  name: "JavaScript",
  abbreviation: "JS",
  isAwesome: true,
  officialSpec: "ECMAScript",
  birthYear: 1995,
  creator: "Brendan Eich"
};
Accessing Object Properties

Using dot notation:

console.log(js.name);

Output:

JavaScript

Other examples:

js.abbreviation;
js.birthYear;
js.creator;
Changing Object Properties

Objects declared with const can still have their properties changed.

const indecisive = {
  lunch: "sandwich"
};

indecisive.lunch = "tacos";

Now:

indecisive.lunch;
// "tacos"
Adding Object Properties

New properties can also be added.

indecisive.snack = "chips";

Now the object contains:

{
  lunch: "tacos",
  snack: "chips"
}
Arrays are Objects

JavaScript arrays are technically objects.

typeof {};
// "object"

typeof [];
// "object"

This is why:

typeof [1, 2, 3];
// "object"
Object Exercise

Create an object representing a person.

const anjana = {
  name: "Anjana",
  home: "San Francisco",
  languages: ["English", "German", "French"],
  pet: null,
  vehicle: "Vespa",
  hobbies: ["travel", "climbing", "gaming", "lindy hop"]
};

Accessing values:

anjana.name;
anjana.home;
anjana.languages[0];
anjana.hobbies[2];
Object Methods

A function stored inside an object property is called a method.

Example:

const dog = {
  name: "Ein",
  breed: "Corgi",

  speak: function () {
    console.log("woof woof");
  }
};

Call the method:

dog.speak();

Output:

woof woof
The this Keyword

Inside an object method, this can refer to the object that owns the method.

Example:

const dog = {
  name: "Ein",

  greet: function () {
    console.log("Hi, I'm " + this.name + "!");
  }
};

dog.greet();

Output:

Hi, I'm Ein!

Here:

this.name

refers to:

dog.name
Adding a Method Later

A method can also be added after the object has been created.

anjana.speak = function () {
  console.log("Hi my name is", this.name);
};

anjana.speak();
Object Methods Exercise

Add a greet() method to the dog object.

dog.greet = function () {
  console.log("Hi, I'm " + this.name + "!");
};

dog.greet();
Object.freeze()

Object.freeze() prevents changes to an object.

Example:

const user = {
  name: "Ali",
  age: 20
};

Object.freeze(user);

After freezing, attempts to:

Add properties
Change properties
Delete properties

are prevented.

Example:

user.age = 21;
user.city = "Jenin";

The object remains frozen.

Check whether an object is frozen:

Object.isFrozen(user);
Built-in JavaScript Objects

JavaScript provides many built-in objects.

Math
Math.max(3, 7, 2);
// 7

Math.round(4.6);
// 5
Date
const date = new Date();

Creates a Date object representing the current date and time.

JSON

JavaScript provides JSON methods for converting between JavaScript objects and JSON strings.

const user = {
  name: "Ali"
};

const json = JSON.stringify(user);

Result:

'{"name":"Ali"}'
Console Methods

The console provides useful methods for debugging.

console.log("Hello");

Warning:

console.warn("Something may be wrong");

These messages can be viewed in the browser DevTools console.

Strings and Wrapper Objects

Strings are primitive values.

However, JavaScript allows us to use methods on strings:

const text = "Hello";

text.length;
text.indexOf("e");
text.toUpperCase();

JavaScript temporarily provides an object-like wrapper so these methods can be used.

The original string remains immutable.

For example:

let text = "Hello";

text[0] = "Y";

The string itself cannot be directly modified this way.

Nested Objects

Objects can contain other objects.

Example:

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

Access nested properties:

const tiramisu = menu.lunch.dessert;

console.log(tiramisu);
// "tiramisu"
Nested Arrays and Objects

Objects and arrays can be combined.

Example:

const spiceGirls = {
  motto: "Girl Power",

  members: [
    {
      name: "Melanie",
      nickname: "Scary"
    },
    {
      name: "Geri",
      nickname: "Ginger"
    }
  ],

  albums: [
    "Spice",
    "Spiceworld"
  ]
};

Access values:

spiceGirls.motto;

spiceGirls.members[1];

spiceGirls.albums[1];

spiceGirls.members[1].name;

Nested data is very common in real JavaScript applications.

Section 7 — Functions

Functions are reusable blocks of code designed to perform a task.

Basic function:

function greet() {
  console.log("Hello!");
}

Call the function:

greet();
Function Parameters

Parameters are variables defined in the function declaration.

function greet(name) {
  console.log("Hello " + name);
}

Call:

greet("Ali");

Output:

Hello Ali
Function Arguments

An argument is the value passed to a function when it is called.

greet("Ali");

Here:

name → parameter
"Ali" → argument
Functions with Multiple Parameters
function add(a, b) {
  return a + b;
}

Call:

const result = add(3, 4);

console.log(result);
// 7
What Happens if an Argument is Missing?

JavaScript allows a function to be called with fewer arguments than its declared parameters.

Example:

function add(a, b) {
  return a + b;
}

add(5);

The missing parameter receives:

undefined

Therefore:

5 + undefined

results in:

NaN

This is important when working with functions that expect multiple values.

Default Parameters

A default parameter can provide a value when an argument is missing.

function greet(name = "Guest") {
  console.log("Hello " + name);
}

Now:

greet();

Output:

Hello Guest
Functions and Reusability

Instead of repeating code:

console.log("Hello Ali");
console.log("Hello Sara");
console.log("Hello Ahmad");

we can create one reusable function:

function greet(name) {
  console.log("Hello " + name);
}

greet("Ali");
greet("Sara");
greet("Ahmad");

Functions make programs easier to organize and maintain.

Section 8 — Quiz Project

The course combines the concepts learned so far into a small JavaScript quiz.

The project uses:

Variables
Data types
Arrays
Objects
Functions
DOM selection
Event handling
Conditional statements
Updating HTML
Selecting the Result Element

HTML:

<p id="result"></p>

JavaScript:

const result = document.querySelector("#result");
Displaying a Score
const score = 8;

result.textContent = "Your score: " + score;

Output on the webpage:

Your score: 8
Conditional Statements

A condition allows JavaScript to make decisions.

if (score >= 5) {
  console.log("Passed");
} else {
  console.log("Try again");
}
Pass / Fail Exercise

HTML:

<p id="message"></p>

JavaScript:

const message = document.querySelector("#message");

if (score >= 5) {
  message.textContent = "You passed!";
} else {
  message.textContent = "Try again!";
}
Multiple Choice Questions

A quiz can store questions and answers using arrays and objects.

Example:

const questions = [
  {
    question: "What is JavaScript?",
    choices: [
      "A programming language",
      "A database",
      "An operating system"
    ],
    answer: "A programming language"
  }
];

This structure allows the program to store multiple questions.

getMultipleChoices()

A function such as getMultipleChoices() can be used to retrieve or generate the possible answers for a quiz question.

The general idea is:

Question
   ↓
Get choices
   ↓
Display choices
   ↓
User selects an answer
   ↓
Check answer
   ↓
Update score

This demonstrates how functions, arrays, objects, and the DOM can work together.

Quiz Data Flow
Question Data
     ↓
JavaScript
     ↓
Create / Display Choices
     ↓
User Interaction
     ↓
Check Answer
     ↓
Update Score
     ↓
Update DOM
Tic-Tac-Toe Project

The Tic-Tac-Toe example demonstrates how JavaScript concepts can be combined into a small interactive application.

It uses:

Arrays
Objects
Variables
Functions
DOM manipulation
Event handling
User interaction
Application state
Representing the Board

A 3×3 Tic-Tac-Toe board can be represented using an array.

const board = [
  "", "", "",
  "", "", "",
  "", "", ""
];

Each position represents one square.

0 | 1 | 2
---------
3 | 4 | 5
---------
6 | 7 | 8
Updating the Board

If the player selects the center square:

board[4] = "X";

The board becomes:

[
  "", "", "",
  "", "X", "",
  "", "", ""
]
DOM + Board State

The important idea in the Tic-Tac-Toe example is that the array represents the data/state, while the DOM represents what the user sees.

JavaScript Array
      ↓
   Game State
      ↓
   Render Board
      ↓
      DOM
      ↓
   Web Page

When the user clicks a square:

User Click
    ↓
Event Listener
    ↓
Update Array
    ↓
Update DOM
    ↓
Display New Board

This is an important pattern used in larger applications.

Why Separate Data from the DOM?

Keeping the game state in JavaScript makes it easier to:

Check the current board
Determine whose turn it is
Check winning combinations
Reset the game
Update the interface
Add more game logic

Example:

const board = ["", "", "", "", "", "", "", "", ""];

board[4] = "X";

The DOM can then be updated based on the current state of board.

Important JavaScript Concepts

By completing the Tic-Tac-Toe example, several concepts work together:

Arrays
  +
Variables
  +
Functions
  +
Events
  +
DOM
  +
Conditional Logic
  =
Interactive Application
Common JavaScript Concepts to Remember
1. JavaScript is dynamically typed

You do not need to specify a variable's type explicitly.

let value = 10;

value = "Hello";

The variable can refer to a value of another type.

2. Arrays start at index 0
const fruits = ["apple", "banana"];

fruits[0];
// apple
3. const does not make objects immutable
const user = {
  name: "Ali"
};

user.name = "Ahmad";

The property can still change.

To prevent modifications:

Object.freeze(user);
4. Arrays and objects use references
const array1 = [1, 2, 3];

const array2 = array1;

array2[0] = 100;

Now:

array1;
// [100, 2, 3]

because both variables refer to the same array.

5. === is usually preferred

Instead of:

5 == "5";

prefer:

5 === "5";

Strict equality checks both the value and the type.

6. DOM changes are not permanent

Changing:

document.querySelector("h1").textContent = "Hello";

changes the current page.

Refreshing the page reloads the original HTML.

Quick Review
Topic	Main Idea
JavaScript	Adds behavior and interactivity
document	Represents the current webpage
DOM	Tree representation of HTML
querySelector()	Selects the first matching element
querySelectorAll()	Selects all matching elements
getElementById()	Selects an element by ID
getElementsByTagName()	Selects elements by tag
getElementsByClassName()	Selects elements by class
.length	Returns the number of items/characters
.textContent	Reads or changes text
Events	Allow JavaScript to react to user actions
String	Represents text
Number	Represents numeric values
Boolean	true or false
undefined	A value has not been assigned
null	Intentional absence of a value
typeof	Checks the type of a value
Operators	Perform calculations and comparisons
Expression	Produces a value
Statement	Performs an action/control flow
let	Variable that can be reassigned
const	Variable that cannot be reassigned
Array	Ordered collection of values
Object	Collection of related properties
Method	Function stored as an object property
this	Refers to the relevant object in a method
Object.freeze()	Prevents changes to an object
Function	Reusable block of code
Parameter	Variable defined by a function
Argument	Value passed to a function
Quiz	Combines JavaScript and DOM concepts
Tic-Tac-Toe	Demonstrates state + DOM interaction
Practice Checklist

Use this checklist to review the course:

 I can explain what JavaScript is.
 I can run JavaScript in the browser console.
 I can connect an external .js file to HTML.
 I understand the DOM.
 I can select elements using querySelector().
 I can select multiple elements using querySelectorAll().
 I understand getElementById().
 I understand getElementsByTagName().
 I understand getElementsByClassName().
 I can use .length.
 I can read and change .textContent.
 I can respond to click events.
 I understand JavaScript primitive data types.
 I can use typeof.
 I understand string indexing.
 I can use common string methods.
 I understand arithmetic operators.
 I understand comparison operators.
 I understand == vs ===.
 I understand expressions and statements.
 I can declare and assign variables.
 I understand let and const.
 I can create and modify arrays.
 I understand array indexes.
 I can use common array methods.
 I understand shared references.
 I can create objects.
 I can access object properties.
 I can add and modify properties.
 I understand object methods.
 I understand this.
 I understand nested objects.
 I understand Object.freeze().
 I can create functions.
 I understand parameters and arguments.
 I understand what happens when arguments are missing.
 I can use functions with the DOM.
 I can build a simple quiz.
 I understand how JavaScript state can control a webpage.
 I understand the basic structure of the Tic-Tac-Toe example.
Useful Resources
JavaScript First Steps — Anjana Vakil
Tic-Tac-Toe Example
MDN Web Docs
Final Takeaway

The main goal of this course is to understand how JavaScript works with both data and the webpage.

The fundamental relationship is:

JavaScript
    ↓
Data
    ↓
Arrays / Objects / Variables
    ↓
Functions
    ↓
DOM
    ↓
User Interaction
    ↓
Interactive Web Application

Once these concepts are understood, they become the foundation for learning more advanced JavaScript topics such as:

Loops
Advanced functions
Scope
Closures
Events
Asynchronous JavaScript
Promises
Fetch API
Modules
Classes
Modern JavaScript frameworks
