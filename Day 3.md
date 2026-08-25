# JavaScript First Steps - Day 3

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

Day 3 felt like a step up from the first two days. It started getting into the stuff that actually makes web pages interactive.

Main topics covered:

- Events
- Conditionals
- Loops
- `map()` and `filter()`
- Spread syntax
- Fetch
- Promises
- Async/Await
- Destructuring
- Modules
- Debugging
- Error handling

There was also a big practical project: the **Doggo Quiz**.

The idea is pretty simple — grab a dog image from an API, figure out the breed from the URL, create multiple choices, and let the user guess. Then check if they got it right or wrong.

The big picture flow to keep in mind:

```text
User action
   ↓
Event handler
   ↓
Function
   ↓
Fetch data
   ↓
Process data
   ↓
Update DOM
```

---

## 2. Events and Handlers Review

An event is something that happens on the page, like:

- click
- mouse movement
- keyboard press
- form submit

JavaScript can listen for a specific event using `addEventListener()`.

```js
const button = document.querySelector("button");

button.addEventListener("click", function () {
  console.log("Button clicked");
});
```

Here `"click"` is the event type, and the function is the handler — basically the code that runs when the event happens.

Another example:

```js
button.addEventListener("mouseover", function () {
  console.log("Mouse is over the button");
});
```

### Event Object

The handler can receive an object with info about the event.

```js
button.addEventListener("click", function (event) {
  console.log(event);
});
```

One of the most useful properties is `event.target`, which is usually the element that triggered the event.

For example, with quiz buttons:

```js
button.addEventListener("click", function (event) {
  console.log(event.target.textContent);
});
```

This makes it easy to figure out which button was actually clicked.

---

## 3. Conditionals Review

Conditionals let the program make decisions based on a condition.

```js
const score = 8;

if (score >= 5) {
  console.log("You passed");
} else {
  console.log("Try again");
}
```

In the quiz this was used to compare the user's guess with the correct answer:

```js
if (guess === correctAnswer) {
  console.log("Correct");
} else {
  console.log("Incorrect");
}
```

### Truthy and Falsy

JavaScript treats some values as `false` inside a condition. The main falsy values are:

```js
false
0
""
null
undefined
NaN
```

Example:

```js
const username = "";

if (username) {
  console.log("Username exists");
} else {
  console.log("Username is empty");
}
```

Since `username` is an empty string, it goes straight to `else`. This can be a bit tricky at first because the string exists but it's still falsy.

### Logical Operators

#### `&&`

Both conditions need to be true.

```js
if (age >= 18 && hasID) {
  console.log("Access allowed");
}
```

#### `||`

Only one condition needs to be true.

```js
if (isStudent || hasCoupon) {
  console.log("Discount available");
}
```

#### `!`

Flips the boolean.

```js
const isCorrect = false;
console.log(!isCorrect); // true
```

### Ternary Operator

A shorter way to write `if...else`.

```js
const message = score >= 5 ? "You passed" : "Try again";
```

Format: `condition ? valueIfTrue : valueIfFalse`

---

## 4. Loops Review

Loops are for repeating the same code multiple times.

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

Three parts to remember: initial value → condition → update.

### For...of

When working with an array and just going through each value, `for...of` is cleaner.

```js
const breeds = ["beagle", "poodle", "boxer"];

for (const breed of breeds) {
  console.log(breed);
}
```

No need to deal with the index unless it's actually needed.

In the quiz this was useful for adding event listeners to all buttons:

```js
const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", handleGuess);
}
```

And for disabling them all:

```js
for (const button of buttons) {
  button.disabled = true;
}
```

---

## 5. Map and Filter

These two array methods came up a lot today.

### map()

`map()` is for transforming **every element** in an array into something new.

```js
const numbers = [1, 2, 3];

const doubled = numbers.map((number) => number * 2);

console.log(doubled); // [2, 4, 6]
```

Another example:

```js
const dogs = [
  { name: "Mochi", breed: "poodle" },
  { name: "Bingo", breed: "beagle" },
  { name: "Rex", breed: "boxer" },
];

const names = dogs.map((dog) => dog.name);

console.log(names); // ["Mochi", "Bingo", "Rex"]
```

### filter()

`filter()` is different — it picks only the elements that match a condition. Nothing gets changed, just filtered.

```js
const numbers = [3, 8, 12, 4];

const largeNumbers = numbers.filter((number) => number > 5);

console.log(largeNumbers); // [8, 12]
```

Another example:

```js
const nicknames = ["Anny", "Mo", "Jenny", "Lee"];

const namesEndingInY = nicknames.filter((name) =>
  name.endsWith("y")
);

console.log(namesEndingInY); // ["Anny", "Jenny"]
```

### Quick Difference

| Method     | Use it when...                           |
| ---------- | ---------------------------------------- |
| `map()`    | Need to change/transform every element   |
| `filter()` | Need to keep only elements that match    |

---

## 6. Spread Syntax

Spread syntax looks like this: `...`

It's used a lot with arrays.

```js
const first = ["a", "b"];
const second = ["c", "d"];

const combined = [...first, ...second];

console.log(combined); // ["a", "b", "c", "d"]
```

It can also copy an array:

```js
const original = ["poodle", "beagle"];
const copy = [...original];
```

Or add an element without touching the original:

```js
const choices = ["poodle", "beagle"];
const moreChoices = [...choices, "boxer"];
```

One thing to be careful about: spread is **not** a deep copy.

```js
const nested = [{ name: "Mochi" }];
const copy = [...nested];

copy[0].name = "Bingo";

console.log(nested[0].name); // "Bingo"
```

The array itself was copied, but the object inside is still shared. This is easy to miss.

---

## 7. Doggo Quiz Game

This project pulled together most of the concepts from today.

The idea: get a dog image from an API, ask the user to guess the breed.

The steps look something like this:

```text
Get dog image
     ↓
Find breed from URL
     ↓
Create choices
     ↓
Show image
     ↓
Show buttons
     ↓
User clicks
     ↓
Check answer
     ↓
Show result
```

The project used a bit of everything: API, arrays, loops, random values, DOM, event listeners, async/await, and conditionals.

---

## 8. While Loops

A `while` loop keeps repeating as long as the condition is true.

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

In the Doggo Quiz this was useful for generating random choices:

```js
const choices = [correctAnswer];

while (choices.length < 4) {
  const choice = getRandomElement(allBreeds);

  if (!choices.includes(choice)) {
    choices.push(choice);
  }
}
```

It starts with the correct answer, then keeps adding random ones until there are 4.

**Important:** Something inside the loop needs to change the condition. Otherwise it becomes an infinite loop and the page freezes. Definitely something to watch out for.

---

## 9. Random Choices and Shuffle

To pick a random element from an array:

```js
function getRandomElement(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}
```

The logic behind it:

```text
Math.random()
     ↓
random number between 0 and 1
     ↓
* array.length
     ↓
Math.floor()
     ↓
valid array index
```

### Shuffle

After creating the choices, the correct answer shouldn't always be the first button. A shuffle function fixes that:

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

Notice `const copy = [...array]` — this keeps the original array untouched.

---

## 10. Fetch

`fetch()` is how data gets requested from an API.

```js
const response = await fetch(
  "https://dog.ceo/api/breeds/image/random"
);
```

The key thing to understand is that `fetch()` doesn't return the data right away. It returns a **Promise**.

Once the response arrives, the JSON can be read:

```js
const response = await fetch(url);
const body = await response.json();
```

`response.json()` also returns a Promise, so `await` is needed there too. This is easy to forget — both lines need `await`.

Example response:

```js
{
  message: "https://images.dog.ceo/breeds/poodle-standard/n02113799_2280.jpg",
  status: "success"
}
```

The image URL lives inside `body.message`.

---

## 11. Promises

A Promise represents a value that hasn't arrived yet.

It has 3 states:

| State     | Meaning           |
| --------- | ----------------- |
| Pending   | Still waiting     |
| Fulfilled | Done successfully |
| Rejected  | Something failed  |

When writing:

```js
const promise = fetch(url);
```

The final response isn't there yet. What comes back is a Promise that will eventually resolve. This makes sense because an API request takes time.

---

## 12. Await

`await` pauses the code until a Promise finishes.

```js
const response = await fetch(url);
const body = await response.json();
```

The flow:

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
JavaScript object
```

This makes the code read like normal step-by-step code instead of dealing with Promises directly.

`await` can only be used inside an `async function` (or at the top level of a module in modern environments).

---

## 13. Async Functions

To use `await` inside a function, `async` goes in front of it:

```js
async function getDogImage() {
  const response = await fetch(
    "https://dog.ceo/api/breeds/image/random"
  );

  const body = await response.json();

  return body.message;
}
```

Something to keep in mind: an async function itself always returns a Promise.

So this:

```js
const imageUrlPromise = getDogImage();
```

Still gives a Promise. To get the actual value:

```js
const imageUrl = await getDogImage();
```

Cleaner version using destructuring:

```js
async function getDogImageUrl() {
  const response = await fetch(
    "https://dog.ceo/api/breeds/image/random"
  );

  const { message } = await response.json();

  return message;
}
```

---

## 14. Destructuring Data

Destructuring is a shortcut for pulling values out of objects or arrays.

### Object Destructuring

Given this:

```js
const dogData = {
  message: "dog-image.jpg",
  status: "success",
};
```

Instead of:

```js
const message = dogData.message;
const status = dogData.status;
```

It can be shortened to:

```js
const { message, status } = dogData;
```

Now both variables are ready to use.

### Array Destructuring

Same idea with arrays:

```js
const breeds = ["poodle", "beagle", "boxer"];

const [firstBreed, secondBreed] = breeds;

// firstBreed → "poodle"
// secondBreed → "beagle"
```

---

## 15. Working with Dog CEO URLs

The Dog CEO API returns URLs like:

```text
https://images.dog.ceo/breeds/poodle-standard/n02113799_2280.jpg
```

Splitting it:

```js
const urlArray = url.split("/");
```

Gives roughly:

```text
0 → "https:"
1 → ""
2 → "images.dog.ceo"
3 → "breeds"
4 → "poodle-standard"
5 → "n02113799_2280.jpg"
```

So the breed is at index `4`:

```js
const breed = urlArray[4];
```

Or with destructuring:

```js
const [, , , , breed] = url.split("/");
```

### Formatting the Breed

Sometimes the breed looks like `"poodle-standard"` but it should display as `"standard poodle"`.

```js
const breed = "poodle-standard";

const formattedBreed = breed
  .split("-")
  .reverse()
  .join(" ");

console.log(formattedBreed); // "standard poodle"
```

Another example:

```js
const breed = "terrier-border";

const formattedBreed = breed
  .split("-")
  .reverse()
  .join(" ");

console.log(formattedBreed); // "border terrier"
```

---

## 16. Rendering the Doggo Fetch Quiz

Rendering means updating the DOM to show information to the user.

HTML structure:

```html
<h1>Doggo Fetch</h1>
<img id="dog-image" alt="Dog quiz image" />
<div id="options"></div>
<p id="result"></p>
```

Grabbing the elements:

```js
const dogImage = document.querySelector("#dog-image");
const options = document.querySelector("#options");
const result = document.querySelector("#result");
```

### Creating Buttons

A button gets created for each choice:

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

This single function combines loops, DOM manipulation, event listeners, and conditionals. A good example of how everything connects.

### Rendering the Quiz

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

The full picture:

```text
async function
      ↓
fetch API
      ↓
await response
      ↓
parse JSON
      ↓
get useful data
      ↓
extract breed
      ↓
create choices
      ↓
render DOM
      ↓
handle clicks
```

---

## 17. Modules

When a project gets bigger, keeping everything in one file gets messy. The code can be split into separate files:

```text
project/
├── index.html
├── main.js
├── dog-api.js
└── quiz-utils.js
```

For example, in `quiz-utils.js`:

```js
export function getRandomElement(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}
```

Then in `main.js`:

```js
import { getRandomElement } from "./quiz-utils.js";
```

The HTML needs to know it's a module:

```html
<script type="module" src="main.js"></script>
```

Key things to remember about modules:

- `import` and `export` are available
- Each module has its own scope
- Module scripts are deferred by default
- Top-level `await` works in modern environments

A simple way to split things up:

| File            | What goes in it            |
| --------------- | -------------------------- |
| `main.js`       | App startup, wiring things |
| `dog-api.js`    | API functions              |
| `quiz-utils.js` | Random, shuffle            |
| `dom.js`        | DOM-related functions      |

---

## 18. Debugging

Debugging is just finding and fixing problems in the code.

The most common tools:

```js
console.log()
console.warn()
console.error()
debugger
```

### console.log()

For checking what's inside a variable:

```js
console.log("choices:", choices);
console.log("correctAnswer:", correctAnswer);
```

### console.warn()

When something looks off but isn't a full error:

```js
console.warn("No choices were created");
```

### console.error()

For actual errors:

```js
console.error("Could not fetch dog image");
```

### debugger

This can be dropped anywhere in the code:

```js
function getBreedFromURL(url) {
  debugger;
  const [, , , , breed] = url.split("/");
  return breed;
}
```

If DevTools is open, the code pauses at that line and variables can be inspected step by step. Honestly more useful than logging everything to the console.

---

## 19. Try/Catch Error Handling

When working with APIs, things can go wrong:

- API is down
- Internet issues
- Bad response
- Missing data

`try...catch` helps handle those situations:

```js
try {
  // code that might fail
} catch (error) {
  // handle the error
}
```

Real example:

```js
async function getDogImageUrl() {
  try {
    const response = await fetch(
      "https://dog.ceo/api/breeds/image/random"
    );

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

Then when rendering, check for `null`:

```js
async function renderQuiz() {
  const imageUrl = await getDogImageUrl();

  if (!imageUrl) {
    result.textContent =
      "Could not load a dog image. Please try again.";
    return;
  }

  dogImage.src = imageUrl;
}
```

This way the app doesn't just silently break — the user actually sees what went wrong.

---

## 20. Frameworks vs Vanilla JavaScript

Vanilla JavaScript means plain JavaScript without any framework.

Frameworks like React, Vue, Angular, and Svelte exist, but the fundamentals stay the same regardless.

Everything from today still matters no matter what framework gets used later:

- Events
- DOM
- Fetch
- Promises
- Async/Await
- Arrays
- map/filter
- Error handling
- Modules

Understanding what JavaScript itself does comes first. Frameworks just help organize and build on top of these basics.

---

## 21. Complete Mental Model

The big picture after Day 3:

```text
HTML
  ↓
DOM
  ↓
JavaScript selects elements
  ↓
User does something
  ↓
Event handler runs
  ↓
Function handles the logic
  ↓
fetch() requests data
  ↓
Promise
  ↓
await
  ↓
Response
  ↓
JSON
  ↓
Destructuring
  ↓
map / filter
  ↓
spread
  ↓
Process the data
  ↓
Update the DOM
  ↓
User sees the result
```

And for bigger projects:

```text
Modules
   +
Debugging
   +
try/catch
```

These keep the code organized and easier to work with.

---

## 22. Quick Reference

### Event

```js
element.addEventListener("click", handler);
```

### Event Target

```js
function handler(event) {
  console.log(event.target);
}
```

### If / Else

```js
if (condition) {
  // true
} else {
  // false
}
```

### Ternary

```js
const message = isCorrect ? "Correct" : "Incorrect";
```

### For

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

### While

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

### Export

```js
export function helper() {}
```

### Import

```js
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

### 1. Forgetting `await` with `response.json()`

❌

```js
const body = response.json();
```

✅

```js
const body = await response.json();
```

This one is super easy to miss since `fetch` already has an `await`.

### 2. Using `await` outside an async function

`await` only works inside an `async` function (or top-level in a module). Putting it in a regular function will throw an error.

### 3. Confusing `map()` and `filter()`

A simple way to remember:

```text
map → change/transform
filter → choose/keep
```

### 4. Infinite `while` loop

Wrong:

```js
let count = 0;
while (count < 5) {
  console.log(count);
}
```

`count` never changes so the loop never stops. Fixed:

```js
let count = 0;
while (count < 5) {
  console.log(count);
  count++;
}
```

### 5. Forgetting `type="module"`

If the code uses `import`, the script tag needs:

```html
<script type="module" src="main.js"></script>
```

Without it, `import` and `export` won't work.

### 6. Thinking `fetch()` automatically treats 404/500 as errors

It doesn't. The response needs to be checked manually:

```js
if (!response.ok) {
  throw new Error(`Request failed: ${response.status}`);
}
```

### 7. Accidentally modifying the original array

If a copy is needed:

```js
const copy = [...original];
```

### 8. Grabbing the wrong index from the URL

```text
https://images.dog.ceo/breeds/poodle-standard/image.jpg
```

After `url.split("/")`, the breed is at index `[4]`:

```js
const breed = url.split("/")[4];
```

Off-by-one errors here are really common.

---

## 24. Practice Checklist

- [ ] Can add an event listener
- [ ] Understand the event object
- [ ] Can use `event.target`
- [ ] Can write `if...else`
- [ ] Understand truthy and falsy values
- [ ] Can use `&&`, `||`, and `!`
- [ ] Can write a ternary
- [ ] Can write a `for` loop
- [ ] Can use `for...of`
- [ ] Can write a `while` loop without making it infinite
- [ ] Understand `map()`
- [ ] Understand `filter()`
- [ ] Can use spread syntax
- [ ] Can get a random item from an array
- [ ] Can shuffle an array
- [ ] Understand what `fetch()` does
- [ ] Understand why `fetch()` returns a Promise
- [ ] Can use `await`
- [ ] Can use `await response.json()`
- [ ] Can write an `async` function
- [ ] Can destructure objects
- [ ] Can destructure arrays
- [ ] Can split a URL using `.split("/")`
- [ ] Can extract the breed from a Dog CEO URL
- [ ] Can create buttons using JavaScript
- [ ] Can connect button clicks to quiz logic
- [ ] Understand the basic idea of modules
- [ ] Can use `import` and `export`
- [ ] Can use `console.log()` for debugging
- [ ] Understand how `debugger` works
- [ ] Can use `try...catch`
- [ ] Understand the general flow of an API-based JavaScript app
