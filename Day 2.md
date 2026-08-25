
# JavaScript First Steps — Day 2

## Table of Contents

1. [Day 2 Overview](#1-day-2-overview)
2. [Functions](#2-functions)
3. [Parameters and Arguments](#3-parameters-and-arguments)
4. [Return Values](#4-return-values)
5. [Arrow Functions](#5-arrow-functions)
6. [Scope](#6-scope)
7. [`let` vs `var`](#7-let-vs-var)
8. [Events and Event Handlers](#8-events-and-event-handlers)
9. [The Event Object](#9-the-event-object)
10. [Conditionals](#10-conditionals)
11. [Truthy and Falsy](#11-truthy-and-falsy)
12. [Logical Operators](#12-logical-operators)
13. [Ternary Operator](#13-ternary-operator)
14. [Loops](#14-loops)
15. [`for...of`](#15-forof)
16. [Quiz Project Functions](#16-quiz-project-functions)
17. [Looping Through Quiz Buttons](#17-looping-through-quiz-buttons)
18. [`isCorrect(guess)`](#18-iscorrectguess)
19. [Putting the Quiz Together](#19-putting-the-quiz-together)
20. [Quick Reference](#20-quick-reference)
21. [Common Mistakes](#21-common-mistakes)
22. [Practice Checklist](#22-practice-checklist)

---

## 1. Day 2 Overview

Day 2 was where things started getting real. Day 1 was mostly about variables, data types, and basic DOM stuff. Day 2 introduced the building blocks that actually make a page *do* something.

Main topics covered:

- Functions
- Parameters and arguments
- Return values
- Arrow functions
- Scope
- `let` vs `var`
- Events and event handlers
- Conditionals
- Truthy and falsy values
- Logical operators
- Loops

And the big practical part was the **Quiz Project**, which tied all of these together.

By the end of Day 2, the goal is to be able to:

- Declare and call functions
- Pass values into functions and return values back
- Write arrow functions
- Explain scope and the difference between `let`, `const`, and `var`
- Register event handlers with `addEventListener()`
- Use the event object
- Write conditionals and understand truthy/falsy
- Use logical operators and ternary expressions
- Write loops and loop through buttons
- Build quiz logic combining functions, events, conditionals, and loops

The general flow to keep in mind:

```text
Display statement
       ↓
User clicks answer button
       ↓
Event handler runs
       ↓
Read clicked button text
       ↓
Call isCorrect(guess)
       ↓
Use conditional
       ↓
Show result
       ↓
Disable all buttons
```

---

## 2. Functions

A function is basically a reusable block of code. Instead of writing the same instructions over and over, you define them once and call them whenever needed.

```js
function greet() {
  console.log("Hello!");
}

greet();
```

Output:

```text
Hello!
```

Nothing happens until the function is actually called. Defining it just sets it up. Calling it with `greet()` is what makes it run.

Without a function:

```js
console.log("Welcome");
console.log("Welcome");
console.log("Welcome");
```

With a function:

```js
function welcome() {
  console.log("Welcome");
}

welcome();
welcome();
welcome();
```

Same result, but way cleaner. And if you need to change the message later, you only change it in one place.

---

## 3. Parameters and Arguments

These two terms are easy to mix up because they sound like the same thing. They're not.

- **Parameter** — the variable name in the function definition (the placeholder)
- **Argument** — the actual value passed when calling the function (the real data)

```js
function greet(name) {
  console.log("Hello " + name);
}

greet("Reem");
```

`name` is the parameter. `"Reem"` is the argument.

| Term      | What it is                      |
| --------- | ------------------------------- |
| Parameter | Placeholder inside the function |
| Argument  | Real value passed to the call   |

Another example:

```js
function multiply(a, b) {
  return a * b;
}

const result = multiply(4, 5);
console.log(result); // 20
```

One thing that's good to know: if a function is called with fewer arguments than parameters, the missing ones become `undefined`.

```js
function add(a, b) {
  return a + b;
}

console.log(add(5)); // NaN
```

`b` is `undefined`, so `5 + undefined` gives `NaN`. This is the kind of bug that can be hard to track down if you don't know what's happening.

---

## 4. Return Values

`return` sends a value back from the function to wherever it was called.

```js
function add(a, b) {
  return a + b;
}

const total = add(2, 3);
console.log(total); // 5
```

This is different from `console.log()`. `console.log()` just prints something to the console — it doesn't give the value back to the code. `return` actually hands the value back so it can be stored in a variable or used somewhere else.

```js
function isAdult(age) {
  return age >= 18;
}

const answer = isAdult(20);
console.log(answer); // true
```

Now `answer` holds `true` and can be used later in conditionals or anywhere else.

One important thing: once JavaScript hits `return`, the function stops immediately.

```js
function test() {
  return "done";
  console.log("This will not run");
}
```

That `console.log` will never execute. Anything after `return` is dead code.

---

## 5. Arrow Functions

Arrow functions are just a shorter way to write functions. They do the same thing but with less syntax.

Traditional:

```js
function multiply(a, b) {
  return a * b;
}
```

Arrow function:

```js
const multiply = (a, b) => {
  return a * b;
};
```

And if the function is just one expression, it can be shortened even more:

```js
const multiply = (a, b) => a * b;
```

The `return` and the curly braces are implied. It looks weird at first but it grows on you.

Another example:

```js
const longerThan = (array1, array2) => {
  return array1.length > array2.length;
};
```

Short version:

```js
const longerThan = (array1, array2) => array1.length > array2.length;
```

This returns `true` or `false` depending on which array is longer. Clean and readable once you get used to the syntax.

---

## 6. Scope

Scope determines where a variable can be accessed. This is one of those things that seems simple until it isn't.

A variable declared inside a function stays inside that function:

```js
function greet() {
  const message = "Hello";
  console.log(message);
}

greet(); // works fine
```

But trying to access it from outside:

```js
function greet() {
  const message = "Hello";
}

console.log(message); // ReferenceError!
```

`message` doesn't exist outside the function. Trying to access it throws an error.

On the flip side, outer variables *can* be read inside nested code:

```js
const name = "Reem";

function greet() {
  console.log("Hello " + name);
}

greet(); // "Hello Reem"
```

The way to think about it: inner scopes can see outer variables, but outer scopes can't see inner variables. Like a one-way mirror.

Scope helps keep variable names organized and prevents different parts of a program from accidentally interfering with each other.

---

## 7. `let` vs `var`

Both declare variables, but they behave differently when it comes to scope.

`let` is **block-scoped** — it only exists inside the `{ }` block where it was declared:

```js
if (true) {
  let message = "Hello";
  console.log(message); // works
}

console.log(message); // ReferenceError
```

`var` is **function-scoped** — it ignores blocks like `if` and `for` and only cares about functions:

```js
function example() {
  var message = "Hello";
  console.log(message);
}
```

| Keyword | Main behavior                        |
| ------- | ------------------------------------ |
| `const` | Cannot be reassigned                 |
| `let`   | Can be reassigned, block-scoped      |
| `var`   | Older keyword, function-scoped       |

Modern JavaScript pretty much always uses `let` and `const`. `var` is older and can cause confusing bugs because it leaks out of blocks. Good to know it exists, but `let` and `const` are the safer choices.

---

## 8. Events and Event Handlers

Events are things that happen in the browser — clicks, mouse movements, key presses, form submissions, etc.

JavaScript can listen for these events using `addEventListener()`:

```js
const button = document.querySelector("button");

button.addEventListener("click", function () {
  console.log("Button clicked");
});
```

Two parts to this:

- **Event type** — `"click"`, `"mouseover"`, `"mouseout"`, `"keydown"`, `"submit"`, etc.
- **Handler function** — the code that runs when the event happens

You can also define the handler separately:

```js
function handleClick() {
  console.log("Clicked");
}

button.addEventListener("click", handleClick);
```

One really important detail: do **not** call the function when passing it as a handler.

```js
button.addEventListener("click", handleClick);   // correct
button.addEventListener("click", handleClick()); // incorrect — runs immediately!
```

The parentheses `()` call the function right away. Without them, you're just handing the function over as a reference, which is what `addEventListener` expects. This is a super common mistake.

---

## 9. The Event Object

When an event fires, the handler can receive an **event object** with details about what happened.

```js
button.addEventListener("click", function (event) {
  console.log(event);
});
```

This object has a lot of properties, but one of the most useful is `event.target` — the actual element that triggered the event.

```js
button.addEventListener("click", function (event) {
  console.log(event.target);
});
```

In the Quiz Project, this is how the code figures out which button the user clicked and what answer they picked:

```js
function handleGuess(event) {
  const guess = event.target.textContent;
  console.log(guess);
}
```

So if the user clicks a button that says "true", `event.target.textContent` gives back `"true"`. Pretty powerful for something that looks so simple.

---

## 10. Conditionals

Conditionals let the code make decisions.

```js
const score = 8;

if (score >= 5) {
  console.log("You passed");
} else {
  console.log("Try again");
}
```

In the quiz:

```js
if (guess === correctAnswer) {
  console.log("Correct");
} else {
  console.log("Incorrect");
}
```

The condition inside the `if` gets evaluated to `true` or `false`. If it's `true`, the first block runs. If it's `false`, the `else` block runs. Straightforward but essential.

---

## 11. Truthy and Falsy

This is one of those JavaScript quirks that takes a moment to get used to.

When JavaScript evaluates a value in a condition, it doesn't just look for `true` or `false`. It treats *every* value as either truthy or falsy.

The falsy values (the ones treated as `false`):

```js
false
0
""
null
undefined
NaN
```

Everything else is truthy.

Example:

```js
const username = "";

if (username) {
  console.log("Username exists");
} else {
  console.log("No username");
}
```

`username` is an empty string, which is falsy, so it goes to `else`. Even though the variable exists and has a value, JavaScript treats `""` as false.

```js
if ("hello") {
  console.log("This runs");
}
```

A non-empty string is truthy. This is really handy for quick checks but can cause bugs if you're not aware of it.

---

## 12. Logical Operators

### AND — `&&`

Both conditions must be true:

```js
if (age >= 18 && hasID) {
  console.log("Access allowed");
}
```

If either one is false, the whole thing is false.

### OR — `||`

At least one condition must be true:

```js
if (isStudent || hasCoupon) {
  console.log("Discount available");
}
```

Only one needs to be true for the whole thing to be true.

### NOT — `!`

Flips a boolean:

```js
const isCorrect = false;
console.log(!isCorrect); // true
```

These come up a lot in conditionals and are essential for combining multiple checks.

---

## 13. Ternary Operator

The ternary operator is a compact way to write an `if...else` in a single line.

```js
const message = score >= 5 ? "You passed" : "Try again";
```

The format:

```text
condition ? valueIfTrue : valueIfFalse
```

Quiz example:

```js
const result = isCorrect(guess) ? "Correct" : "Incorrect";
```

It's not always better than a regular `if...else`. If the logic is complex, a full `if...else` is easier to read. But for simple either/or situations, the ternary is great.

---

## 14. Loops

Loops repeat code so you don't have to write the same thing multiple times.

### `for` Loop

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

Three parts:

```text
initialization (let i = 0)
     ↓
condition (i < 5)
     ↓
update (i++)
```

Example with an array:

```js
const names = ["Ali", "Reem", "Sara"];

for (let i = 0; i < names.length; i++) {
  console.log(names[i]);
}
```

### Increment Operators

```js
i++;
```

Same as `i = i + 1`.

```js
score += 1;
```

Same as `score = score + 1`. The `+=` shortcut works with any number.

---

## 15. `for...of`

`for...of` is a simpler loop for going through arrays. No index, no counter — just the values.

```js
const fruits = ["apple", "banana", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

Output:

```text
apple
banana
orange
```

Compared to a regular `for` loop, `for...of` is way cleaner when the index isn't needed. In the Quiz Project this was used a lot for looping through buttons.

---

## 16. Quiz Project Functions

The Quiz Project combines functions and DOM interaction. Instead of putting all the logic in one big block, everything gets split into small functions.

Example data:

```js
const fact = {
  statement: "JavaScript was created in 1995.",
  answer: "true",
};
```

Render the statement:

```js
const statement = document.querySelector("#statement");
statement.textContent = fact.statement;
```

Create a function to check the answer:

```js
function isCorrect(guess) {
  return guess === fact.answer;
}
```

Use the function:

```js
console.log(isCorrect("true"));  // true
console.log(isCorrect("false")); // false
```

Functions make each piece of logic easier to test and reuse. The function name itself reads like a question: "is this correct?" — which makes the code much more readable.

---

## 17. Looping Through Quiz Buttons

A quiz usually has multiple buttons. Instead of adding an event listener to each one manually, a loop handles all of them.

HTML:

```html
<button>true</button>
<button>false</button>
```

JavaScript:

```js
const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", handleGuess);
}
```

What's happening:

```text
buttons array
   ↓
loop through each button
   ↓
button 1 → gets event handler
button 2 → gets event handler
```

When one answer is clicked, all buttons need to be disabled so the user can't click again:

```js
function disableButtons() {
  for (const button of buttons) {
    button.disabled = true;
  }
}
```

This is a great example of why loops matter. Without the loop, every button would need its own line of code.

---

## 18. `isCorrect(guess)`

This function is the core of the quiz logic.

```js
function isCorrect(guess) {
  return guess === fact.answer;
}
```

If the fact is:

```js
const fact = {
  answer: "true",
};
```

Then:

```js
isCorrect("true");  // true
isCorrect("false"); // false
```

Because it returns a Boolean, it works perfectly inside an `if...else`:

```js
if (isCorrect(guess)) {
  console.log("Correct");
} else {
  console.log("Incorrect");
}
```

What's nice about this setup is that the checking logic is completely separate from the display logic. The function just returns `true` or `false`. Something else decides what to do with that answer.

---

## 19. Putting the Quiz Together

This is where everything from Day 2 comes together into one working app.

HTML:

```html
<p id="statement"></p>
<button>true</button>
<button>false</button>
<p id="result"></p>
```

JavaScript:

```js
const fact = {
  statement: "JavaScript can change the DOM.",
  answer: "true",
};

const statement = document.querySelector("#statement");
const result = document.querySelector("#result");
const buttons = document.querySelectorAll("button");

statement.textContent = fact.statement;

function isCorrect(guess) {
  return guess === fact.answer;
}

function disableButtons() {
  for (const button of buttons) {
    button.disabled = true;
  }
}

function handleGuess(event) {
  const guess = event.target.textContent;

  if (isCorrect(guess)) {
    result.textContent = "Correct";
    event.target.classList.add("correct");
  } else {
    result.textContent = "Incorrect";
    event.target.classList.add("incorrect");
  }

  disableButtons();
}

for (const button of buttons) {
  button.addEventListener("click", handleGuess);
}
```

Flow:

```text
Display statement
       ↓
User clicks answer button
       ↓
Event handler runs
       ↓
Read clicked button text
       ↓
Call isCorrect(guess)
       ↓
Use conditional
       ↓
Show result
       ↓
Disable all buttons
```

This single block of code uses functions, parameters, return values, events, the event object, conditionals, loops, and DOM manipulation. Individually each concept is small, but together they make a fully interactive app. Seeing all these pieces connect was the biggest takeaway from Day 2.

---

## 20. Quick Reference

### Function

```js
function greet(name) {
  return "Hello " + name;
}
```

### Arrow Function

```js
const greet = (name) => "Hello " + name;
```

### Event Listener

```js
element.addEventListener("click", handler);
```

### Event Object

```js
function handler(event) {
  console.log(event.target);
}
```

### Conditional

```js
if (condition) {
  // true
} else {
  // false
}
```

### Logical Operators

```js
&&  // and
||  // or
!   // not
```

### Ternary

```js
const message = condition ? "yes" : "no";
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

---

## 21. Common Mistakes

### 1. Calling a Handler Immediately

❌

```js
button.addEventListener("click", handleGuess());
```

This runs `handleGuess` right away instead of waiting for the click.

✅

```js
button.addEventListener("click", handleGuess);
```

No parentheses — just pass the function reference.

### 2. Forgetting to Return a Value

❌

```js
function isCorrect(guess) {
  guess === fact.answer;
}
```

This compares the values but throws the result away. The function returns `undefined`.

✅

```js
function isCorrect(guess) {
  return guess === fact.answer;
}
```

### 3. Confusing Parameters and Arguments

```js
function greet(name) {} // name = parameter
greet("Reem");          // "Reem" = argument
```

Parameters go in the definition. Arguments go in the call.

### 4. Using Assignment Instead of Comparison

❌

```js
if (guess = fact.answer) {}
```

This *assigns* the value instead of comparing it. The condition will always be truthy (unless the answer is a falsy value).

✅

```js
if (guess === fact.answer) {}
```

Triple equals for comparison. Single equals for assignment. Mixing these up is one of the most common bugs in JavaScript.

### 5. Forgetting to Update a Loop Counter

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

The `i++` matters because it moves the loop toward finishing. Without it, the loop runs forever.

### 6. Forgetting to Call the Function

❌

```js
function greet() {
  console.log("Hello");
}

greet; // nothing happens
```

✅

```js
greet(); // "Hello"
```

The parentheses are what actually run the function.

### 7. Thinking `console.log()` Is the Same as `return`

`console.log()` prints to the console. `return` gives a value back to the code. They're completely different things. A function with only `console.log()` returns `undefined`.

---

## 22. Practice Checklist

- [ ] Can define a function
- [ ] Can call a function
- [ ] Can explain parameters
- [ ] Can explain arguments
- [ ] Can return a value from a function
- [ ] Can write an arrow function
- [ ] Understand function scope
- [ ] Understand block scope
- [ ] Understand `let`, `const`, and `var`
- [ ] Can add an event listener
- [ ] Can use the event object
- [ ] Can read `event.target`
- [ ] Can write `if...else`
- [ ] Understand truthy and falsy values
- [ ] Can use `&&`, `||`, and `!`
- [ ] Can use a ternary expression
- [ ] Can write a `for` loop
- [ ] Can write a `for...of` loop
- [ ] Can loop through buttons
- [ ] Can disable buttons after an answer
- [ ] Can write `isCorrect(guess)`
- [ ] Can combine functions, events, conditionals, and loops in a project

---

