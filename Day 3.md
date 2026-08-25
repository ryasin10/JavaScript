# JavaScript First Steps - Day 3

A detailed learning guide for Day 3 of JavaScript First Steps, based on the attached course materials, the JavaScript First Steps companion site, and MDN Web Docs.

Day 3 connects earlier JavaScript fundamentals to real browser projects. The main focus is working with events, loops, array methods, asynchronous JavaScript, APIs, promises, `fetch()`, `await`, destructuring, modules, and debugging.

## Table of Contents

1. [Day 3 Overview](#1-day-3-overview)
2. [Events and Handlers Review](#2-events-and-handlers-review)
3. [Conditionals Review](#3-conditionals-review)
4. [Loops Review](#4-loops-review)
5. [Map and Filter](#5-map-and-filter)
6. [Spread Syntax](#6-spread-syntax)
7. [Doggo Quiz Game](#7-doggo-quiz-game)
8. [While Loops](#8-while-loops)
9. [Random Choices and Shuffle](#9-random-choices-and-shuffle)
10. [Fetch](#10-fetch)
11. [Promises](#11-promises)
12. [Await](#12-await)
13. [Async Functions](#13-async-functions)
14. [Destructuring Data](#14-destructuring-data)
15. [Working with Dog CEO URLs](#15-working-with-dog-ceo-urls)
16. [Rendering the Doggo Fetch Quiz](#16-rendering-the-doggo-fetch-quiz)
17. [Modules](#17-modules)
18. [Debugging](#18-debugging)
19. [Try/Catch Error Handling](#19-trycatch-error-handling)
20. [Frameworks vs Vanilla JavaScript](#20-frameworks-vs-vanilla-javascript)
21. [Complete Mental Model](#21-complete-mental-model)
22. [Quick Reference](#22-quick-reference)
23. [Common Beginner Mistakes](#23-common-beginner-mistakes)
24. [Practice Checklist](#24-practice-checklist)

---

## 1. Day 3 Overview

Day 3 moves from basic JavaScript syntax into full interactive browser logic.

The official course companion site lists Part 3 topics as:

- Fetch
- Promises
- Async/Await
- Map and Filter
- Destructuring and spread syntax
- Debugging and error handling
- Modules, import, and export

The attached Day 3 notes also include practice with:

- Event listeners
- The event object
- Conditionals
- Logical and ternary operators
- Loops
- Doggo quiz setup
- Choice generation
- Rendering buttons
- Extracting dog breed names from image URLs

The goal is to understand how JavaScript can request data from an API, process that data, and update the DOM to create an interactive web page.

---

## 2. Events and Handlers Review

An event is something that happens in the browser. Examples include a click, a mouse movement, a key press, or a form submission.

JavaScript can listen for events with `addEventListener()`.

```js
const button = document.querySelector("button");

button.addEventListener("click", function () {
  console.log("Button clicked");
});
```

The first argument is the event type.

```js
"click"
"mouseover"
"mouseout"
"keydown"
"submit"
```

The second argument is the handler function. The handler runs when the event happens.

```js
button.addEventListener("mouseover", function () {
  console.log("Mouse is over the button");
});
```

### Event Object

An event handler can receive an event object.

```js
button.addEventListener("click", function (event) {
  console.log(event);
});
```

The event object contains information about what happened. A very useful property is `event.target`, which usually refers to the element that triggered the event.

```js
button.addEventListener("click", function (event) {
  console.log(event.target.textContent);
});
```

In a quiz project, `event.target` can help identify which answer button the user clicked.

---

## 3. Conditionals Review

Conditionals let code make decisions.

```js
const score = 8;

if (score >= 5) {
  console.log("You passed");
} else {
  console.log("Try again");
}
```

In a quiz, a conditional can decide whether a clicked answer is correct.

```js
if (guess === correctAnswer) {
  console.log("Correct");
} else {
  console.log("Incorrect");
}
```

### Truthy and Falsy

JavaScript converts values to Boolean-like meanings in conditions.

Falsy values include:

```js
false
0
""
null
undefined
NaN
```

Everything else is generally truthy.

```js
const username = "";

if (username) {
  console.log("Username exists");
} else {
  console.log("Username is empty");
}
```

### Logical Operators

Use `&&` when both conditions must be true.

```js
if (age >= 18 && hasID) {
  console.log("Access allowed");
}
```

Use `||` when at least one condition must be true.

```js
if (isStudent || hasCoupon) {
  console.log("Discount available");
}
```

Use `!` to reverse a Boolean.

```js
const isCorrect = false;
console.log(!isCorrect); // true
```

### Ternary Operator

A ternary is a compact conditional expression.

```js
const message = score >= 5 ? "You passed" : "Try again";
```

General structure:

```text
condition ? valueIfTrue : valueIfFalse
```

---

## 4. Loops Review

Loops repeat code.

### For Loop

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

Output:

```text
0
1
2
3
4
```

The loop has three main parts:

```text
initial value -> condition -> update
```

### For...of Loop

`for...of` loops through the values in an array.

```js
const breeds = ["beagle", "poodle", "boxer"];

for (const breed of breeds) {
  console.log(breed);
}
```

This is useful when you do not need the numeric index.

### Looping Through Buttons

In a quiz project, you may have several answer buttons.

```js
const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", handleGuess);
}
```

You can also disable all buttons after one answer is selected.

```js
for (const button of buttons) {
  button.disabled = true;
}
```

---

## 5. Map and Filter

`map()` and `filter()` are array methods. They are useful when transforming or selecting data.

### `map()`

`map()` creates a new array by running a function on every item in an existing array.

```js
const numbers = [1, 2, 3];
const doubled = numbers.map((number) => number * 2);

console.log(doubled); // [2, 4, 6]
```

Example with names:

```js
const dogs = [
  { name: "Mochi", breed: "poodle" },
  { name: "Bingo", breed: "beagle" },
  { name: "Rex", breed: "boxer" },
];

const names = dogs.map((dog) => dog.name);

console.log(names); // ["Mochi", "Bingo", "Rex"]
```

### `filter()`

`filter()` creates a new array containing only the items that pass a test.

```js
const numbers = [3, 8, 12, 4];
const largeNumbers = numbers.filter((number) => number > 5);

console.log(largeNumbers); // [8, 12]
```

Example with strings:

```js
const nicknames = ["Anny", "Mo", "Jenny", "Lee"];
const namesEndingInY = nicknames.filter((name) => name.endsWith("y"));

console.log(namesEndingInY); // ["Anny", "Jenny"]
```

### Map vs Filter

| Method | Purpose | Result |
| --- | --- | --- |
| `map()` | Transform every item | New array with same length |
| `filter()` | Keep matching items | New array with same or shorter length |

---

## 6. Spread Syntax

Spread syntax uses `...` to expand an iterable, such as an array, into individual values.

```js
const first = ["a", "b"];
const second = ["c", "d"];

const combined = [...first, ...second];

console.log(combined); // ["a", "b", "c", "d"]
```

It is useful for copying arrays.

```js
const original = ["poodle", "beagle"];
const copy = [...original];
```

It is also useful for adding items without changing the original array.

```js
const choices = ["poodle", "beagle"];
const moreChoices = [...choices, "boxer"];
```

Spread does not deeply clone nested objects or arrays.

```js
const nested = [{ name: "Mochi" }];
const copy = [...nested];

copy[0].name = "Bingo";

console.log(nested[0].name); // "Bingo"
```

The array was copied, but the object inside it was still shared.

---

## 7. Doggo Quiz Game

The Doggo Quiz Game asks the user to identify a dog breed from an image.

The project combines:

- API data
- Random choice generation
- Arrays
- Loops
- DOM rendering
- Event listeners
- Async functions
- Conditional feedback

General flow:

```text
Fetch dog image
      ↓
Extract correct breed from URL
      ↓
Create multiple choices
      ↓
Render dog image
      ↓
Render answer buttons
      ↓
User clicks a choice
      ↓
Check answer
      ↓
Show correct or incorrect state
```

---

## 8. While Loops

A `while` loop repeats while a condition is true.

```js
let count = 0;

while (count < 3) {
  console.log(count);
  count++;
}
```

Output:

```text
0
1
2
```

A `while` loop is useful when you do not know exactly how many tries will be needed.

In the Doggo Quiz, a `while` loop can keep selecting random breeds until the choices array has enough unique options.

```js
const choices = [correctAnswer];

while (choices.length < 4) {
  const choice = getRandomElement(allBreeds);

  if (!choices.includes(choice)) {
    choices.push(choice);
  }
}
```

Important: always make sure a `while` loop can eventually stop. If the condition always stays true, the browser can freeze.

---

## 9. Random Choices and Shuffle

The quiz needs multiple choices, including the correct answer.

```js
function getRandomElement(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}
```

This function:

1. Generates a random number.
2. Multiplies it by the array length.
3. Rounds down with `Math.floor()`.
4. Uses the result as an array index.

Example:

```js
const breeds = ["beagle", "poodle", "boxer"];
const randomBreed = getRandomElement(breeds);
```

### Shuffle

After choices are created, shuffle them so the correct answer is not always first.

```js
function shuffle(array) {
  const copy = [...array];

  for (let i = copy.length - 1; i > 0; i--) {
    const randomIndex = Math.floor(Math.random() * (i + 1));
    const current = copy[i];

    copy[i] = copy[randomIndex];
    copy[randomIndex] = current;
  }

  return copy;
}
```

This returns a shuffled copy instead of changing the original array.

---

## 10. Fetch

`fetch()` lets JavaScript make HTTP requests.

Basic example:

```js
const response = await fetch("https://dog.ceo/api/breeds/image/random");
```

`fetch()` returns a promise. The promise eventually gives a `Response` object.

To read JSON from the response:

```js
const response = await fetch("https://dog.ceo/api/breeds/image/random");
const body = await response.json();
```

`response.json()` also returns a promise, so it needs `await`.

Example response from the Dog CEO API:

```js
{
  message: "https://images.dog.ceo/breeds/poodle-standard/n02113799_2280.jpg",
  status: "success"
}
```

The `message` property contains the image URL.

---

## 11. Promises

A promise represents a value that may be available later.

It can be:

| State | Meaning |
| --- | --- |
| Pending | Still waiting |
| Fulfilled | Completed successfully |
| Rejected | Failed |

`fetch()` returns a promise because the browser has to wait for the network request.

```js
const promise = fetch("https://dog.ceo/api/breeds/image/random");
console.log(promise);
```

Without `await`, JavaScript gives you the promise object itself instead of the final data.

---

## 12. Await

`await` pauses an async function until a promise settles.

```js
const response = await fetch(url);
const body = await response.json();
```

The first `await` waits for the HTTP response.

The second `await` waits for the response body to be parsed as JSON.

```text
fetch(url)
   ↓
Promise for Response
   ↓ await
Response object
   ↓ response.json()
Promise for parsed body
   ↓ await
JavaScript object
```

`await` can only be used inside an async function or at the top level of a JavaScript module.

---

## 13. Async Functions

An async function is a function that can use `await`.

```js
async function getDogImage() {
  const response = await fetch("https://dog.ceo/api/breeds/image/random");
  const body = await response.json();

  return body.message;
}
```

Calling an async function returns a promise.

```js
const imageUrlPromise = getDogImage();
```

To get the actual value, use `await`.

```js
const imageUrl = await getDogImage();
```

### Doggo Fetch Example

```js
async function getDogData() {
  const response = await fetch("https://dog.ceo/api/breeds/image/random");
  const body = await response.json();

  return body;
}
```

With destructuring:

```js
async function getDogImageUrl() {
  const response = await fetch("https://dog.ceo/api/breeds/image/random");
  const { message } = await response.json();

  return message;
}
```

---

## 14. Destructuring Data

Destructuring lets you extract values from arrays or objects into variables.

### Object Destructuring

```js
const dogData = {
  message: "https://images.dog.ceo/breeds/poodle-standard/image.jpg",
  status: "success",
};

const { message, status } = dogData;
```

This creates two variables:

```js
console.log(message);
console.log(status);
```

### Array Destructuring

```js
const breeds = ["poodle", "beagle", "boxer"];
const [firstBreed, secondBreed] = breeds;

console.log(firstBreed); // "poodle"
console.log(secondBreed); // "beagle"
```

Destructuring is helpful when working with API responses because API objects often contain more data than your app needs.

---

## 15. Working with Dog CEO URLs

The Dog CEO API returns image URLs like this:

```text
https://images.dog.ceo/breeds/poodle-standard/n02113799_2280.jpg
```

To extract the breed, split the URL by `/`.

```js
const url = "https://images.dog.ceo/breeds/poodle-standard/n02113799_2280.jpg";
const urlArray = url.split("/");

console.log(urlArray);
```

Result:

```text
Index 0: "https:"
Index 1: ""
Index 2: "images.dog.ceo"
Index 3: "breeds"
Index 4: "poodle-standard"
Index 5: "n02113799_2280.jpg"
```

The breed is at index `4`.

```js
const breed = urlArray[4];
```

### Using Destructuring

```js
const [, , , , breed] = url.split("/");
```

This skips the earlier values and stores the fifth item in `breed`.

### Formatting the Breed Name

Some breed names contain hyphens.

```js
const breed = "poodle-standard";
const formattedBreed = breed.split("-").reverse().join(" ");

console.log(formattedBreed); // "standard poodle"
```

Another example:

```js
const breed = "terrier-border";
const formattedBreed = breed.split("-").reverse().join(" ");

console.log(formattedBreed); // "border terrier"
```

This is useful because the Dog CEO API often stores sub-breeds in a reversed URL format.

---

## 16. Rendering the Doggo Fetch Quiz

Rendering means creating or updating DOM elements so the user can see the current state.

Example HTML:

```html
<h1>Doggo Fetch</h1>
<img id="dog-image" alt="Dog quiz image" />
<div id="options"></div>
<p id="result"></p>
```

Example JavaScript:

```js
const dogImage = document.querySelector("#dog-image");
const options = document.querySelector("#options");
const result = document.querySelector("#result");
```

### Create Choice Buttons

```js
function renderChoices(choicesArray, correctAnswer) {
  options.textContent = "";

  for (const choice of choicesArray) {
    const button = document.createElement("button");
    button.textContent = choice;

    button.addEventListener("click", function () {
      if (choice === correctAnswer) {
        result.textContent = "Correct";
        button.classList.add("correct");
      } else {
        result.textContent = "Incorrect";
        button.classList.add("incorrect");
      }
    });

    options.appendChild(button);
  }
}
```

### Render the Full Quiz

```js
async function renderQuiz() {
  const imageUrl = await getDogImageUrl();
  const correctAnswer = getBreedFromURL(imageUrl);
  const choices = getMultipleChoices(correctAnswer, allBreeds);

  dogImage.src = imageUrl;
  dogImage.alt = `A dog. Guess the breed: ${correctAnswer}`;

  renderChoices(choices, correctAnswer);
}
```

This brings the Day 3 ideas together:

```text
async function
   ↓
fetch API data
   ↓
await response
   ↓
parse JSON
   ↓
destructure data
   ↓
extract breed from URL
   ↓
create choices
   ↓
render DOM
   ↓
handle click events
```

---

## 17. Modules

Modules let you split JavaScript code across multiple files.

Instead of keeping all logic in one large file, you can organize related functions into separate files.

Example structure:

```text
project/
  index.html
  main.js
  dog-api.js
  quiz-utils.js
```

### Export

In `quiz-utils.js`:

```js
export function getRandomElement(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}
```

### Import

In `main.js`:

```js
import { getRandomElement } from "./quiz-utils.js";
```

### Loading a Module in HTML

```html
<script type="module" src="main.js"></script>
```

Module scripts have different behavior from regular scripts:

- They can use `import` and `export`.
- They have their own scope.
- They are deferred by default in the browser.
- They can use top-level `await` in modern environments.

Good module organization:

| File | Responsibility |
| --- | --- |
| `main.js` | Start the app and connect pieces |
| `dog-api.js` | Fetch dog data |
| `quiz-utils.js` | Random choice and shuffle helpers |
| `dom.js` | DOM rendering helpers |

---

## 18. Debugging

Debugging means finding and fixing errors.

Beginner-friendly debugging tools include:

```js
console.log()
console.warn()
console.error()
debugger
```

### `console.log()`

Use `console.log()` to inspect values.

```js
console.log("choices:", choices);
console.log("correctAnswer:", correctAnswer);
```

### `console.warn()`

Use `console.warn()` for suspicious but non-fatal situations.

```js
console.warn("No choices were created");
```

### `console.error()`

Use `console.error()` when something failed.

```js
console.error("Could not fetch dog image");
```

### `debugger`

The `debugger` statement pauses code execution when DevTools is open.

```js
function getBreedFromURL(url) {
  debugger;
  const [, , , , breed] = url.split("/");
  return breed;
}
```

This lets you inspect variables line by line.

---

## 19. Try/Catch Error Handling

Network requests can fail. APIs can be unavailable. Data can be missing.

`try...catch` helps your program handle errors instead of crashing silently.

```js
async function getDogImageUrl() {
  try {
    const response = await fetch("https://dog.ceo/api/breeds/image/random");

    if (!response.ok) {
      throw new Error(`Request failed: ${response.status}`);
    }

    const { message } = await response.json();
    return message;
  } catch (error) {
    console.error(error);
    return null;
  }
}
```

Then the rendering code can handle a missing result.

```js
async function renderQuiz() {
  const imageUrl = await getDogImageUrl();

  if (!imageUrl) {
    result.textContent = "Could not load a dog image. Please try again.";
    return;
  }

  dogImage.src = imageUrl;
}
```

This is better for users because the page can show a helpful message.

---

## 20. Frameworks vs Vanilla JavaScript

Vanilla JavaScript means JavaScript without a framework.

Frameworks like React, Vue, Angular, and Svelte help organize large user interfaces, but they still rely on JavaScript fundamentals.

Day 3 matters because it teaches skills used everywhere:

- Data fetching
- DOM updates
- Event handling
- Array processing
- Async code
- Error handling
- Code organization

Before learning a framework, it helps to understand what the framework is doing for you.

---

## 21. Complete Mental Model

```text
HTML page
   ↓
DOM elements
   ↓
JavaScript selects elements
   ↓
User events trigger handlers
   ↓
Functions organize logic
   ↓
fetch() requests API data
   ↓
Promises represent future values
   ↓
await waits for results
   ↓
JSON becomes JavaScript data
   ↓
Destructuring extracts useful values
   ↓
map/filter process arrays
   ↓
spread copies or combines arrays
   ↓
DOM renders the result
   ↓
Modules organize the project
   ↓
Debugging and try/catch help fix problems
```

---

## 22. Quick Reference

### Events

```js
element.addEventListener("click", handler);
```

### Event Target

```js
function handler(event) {
  console.log(event.target);
}
```

### Conditionals

```js
if (condition) {
  // true path
} else {
  // false path
}
```

### Ternary

```js
const message = isCorrect ? "Correct" : "Incorrect";
```

### For Loop

```js
for (let i = 0; i < array.length; i++) {
  console.log(array[i]);
}
```

### For...of

```js
for (const item of array) {
  console.log(item);
}
```

### While Loop

```js
while (condition) {
  // repeat
}
```

### Map

```js
const newArray = array.map((item) => item.value);
```

### Filter

```js
const filteredArray = array.filter((item) => item.active);
```

### Spread

```js
const copy = [...array];
const combined = [...first, ...second];
```

### Fetch

```js
const response = await fetch(url);
```

### JSON

```js
const body = await response.json();
```

### Promise

```js
const promise = fetch(url);
```

### Async Function

```js
async function loadData() {
  const response = await fetch(url);
  return response.json();
}
```

### Object Destructuring

```js
const { message } = body;
```

### Array Destructuring

```js
const [first, second] = array;
```

### Import and Export

```js
export function helper() {}
import { helper } from "./helper.js";
```

### Try/Catch

```js
try {
  const response = await fetch(url);
} catch (error) {
  console.error(error);
}
```

---

## 23. Common Beginner Mistakes

### 1. Forgetting to Await `response.json()`

Incorrect:

```js
const body = response.json();
```

Correct:

```js
const body = await response.json();
```

### 2. Using `await` Outside an Async Function

Incorrect in a normal script:

```js
const response = await fetch(url);
```

Correct:

```js
async function loadData() {
  const response = await fetch(url);
}
```

### 3. Confusing `map()` and `filter()`

Use `map()` to transform every item.

Use `filter()` to keep only some items.

### 4. Creating an Infinite While Loop

Incorrect:

```js
let count = 0;

while (count < 5) {
  console.log(count);
}
```

`count` never changes, so the loop does not stop.

Correct:

```js
let count = 0;

while (count < 5) {
  console.log(count);
  count++;
}
```

### 5. Forgetting `type="module"`

If a file uses `import`, the HTML must load it as a module.

```html
<script type="module" src="main.js"></script>
```

### 6. Assuming Fetch Throws on HTTP Error Status

`fetch()` may still resolve even if the server responds with an error status like `404`.

Check `response.ok`.

```js
if (!response.ok) {
  throw new Error(`Request failed: ${response.status}`);
}
```

### 7. Mutating an Array Accidentally

If you want a copy, use spread.

```js
const copy = [...original];
```

### 8. Extracting the Wrong URL Index

Given:

```text
https://images.dog.ceo/breeds/poodle-standard/image.jpg
```

After splitting with `/`, the breed is at index `4`.

```js
const breed = url.split("/")[4];
```

---

## 24. Practice Checklist

- [ ] I can add an event listener to a DOM element.
- [ ] I can use the event object.
- [ ] I can read `event.target`.
- [ ] I can write `if...else` statements.
- [ ] I understand truthy and falsy values.
- [ ] I can use `&&`, `||`, and `!`.
- [ ] I can use a ternary expression.
- [ ] I can write a `for` loop.
- [ ] I can write a `for...of` loop.
- [ ] I can write a safe `while` loop.
- [ ] I can use `map()` to transform an array.
- [ ] I can use `filter()` to select items from an array.
- [ ] I can use spread syntax to copy or combine arrays.
- [ ] I can create random choices from an array.
- [ ] I can shuffle an array.
- [ ] I understand what `fetch()` does.
- [ ] I understand why `fetch()` returns a promise.
- [ ] I can use `await` with `fetch()`.
- [ ] I can use `await` with `response.json()`.
- [ ] I can write an async function.
- [ ] I can destructure an object.
- [ ] I can destructure an array.
- [ ] I can split a URL with `.split("/")`.
- [ ] I can extract a dog breed from a Dog CEO image URL.
- [ ] I can render buttons with JavaScript.
- [ ] I can connect button clicks to quiz logic.
- [ ] I can split code into modules.
- [ ] I can use `import` and `export`.
- [ ] I can debug with `console.log()`.
- [ ] I can pause code with `debugger`.
- [ ] I can handle errors with `try...catch`.

---



