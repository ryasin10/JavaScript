# JavaScript First Steps — Day 2

A detailed guide for Day 2, focused on **Functions, Scope, Events, Conditionals, Loops, and the Quiz Project**.

## Table of Contents

1. [Functions](#1-functions)
2. [Parameters and Arguments](#2-parameters-and-arguments)
3. [Return Values](#3-return-values)
4. [Arrow Functions](#4-arrow-functions)
5. [Quiz Project Functions](#5-quiz-project-functions)
6. [Scope](#6-scope)
7. [let vs var](#7-let-vs-var)
8. [Events and Event Handlers](#8-events-and-event-handlers)
9. [Event Object](#9-event-object)
10. [Conditionals](#10-conditionals)
11. [Truthy and Falsy](#11-truthy-and-falsy)
12. [Logical Operators](#12-logical-operators)
13. [Ternary Operator](#13-ternary-operator)
14. [Loops](#14-loops)
15. [for...of](#15-forof)
16. [Quiz Project: Loops and Buttons](#16-quiz-project-loops-and-buttons)
17. [isCorrect(guess)](#17-iscorrectguess)
18. [Quiz Project: Putting Everything Together](#18-quiz-project-putting-everything-together)
19. [Day 2 Summary](#19-day-2-summary)
20. [Practice Checklist](#practice-checklist)
---

# 1. Functions

A **function** is a reusable block of JavaScript code that performs a task. Functions organize code, reduce repetition, accept input, and return results.

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

A function can receive input through a parameter:

```js
function greet(name) {
  console.log("Hello " + name);
}

greet("Reem");
```

Output:

```text
Hello Reem
```

---

# 2. Parameters and Arguments

A **parameter** is the variable defined in the function declaration. An **argument** is the actual value supplied when the function is called.

```js
function multiply(a, b) {
  return a * b;
}

multiply(4, 5);
```

Here `a` and `b` are parameters, while `4` and `5` are arguments.

| Term | Meaning |
|---|---|
| Parameter | Variable representing expected input |
| Argument | Actual value passed to the function |

Example:

```js
function add(firstNumber, secondNumber) {
  return firstNumber + secondNumber;
}

const result = add(10, 20);
console.log(result); // 30
```

---

# 3. Return Values

`return` sends a value back from a function.

```js
function multiply(a, b) {
  return a * b;
}

const result = multiply(4, 5);
console.log(result); // 20
```

Unlike `console.log()`, which displays a value, `return` makes the value available to the calling code.

```js
function add(a, b) {
  return a + b;
}

const answer = add(2, 3);
```

Now `answer` contains `5`.

---

# 4. Arrow Functions

Arrow functions provide another syntax for writing functions.

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

A short version can be used when the function contains one expression:

```js
const multiply = (a, b) => a * b;
```

Example:

```js
const longerThan = (array1, array2) =>
  array1.length > array2.length;
```

---

# 5. Quiz Project Functions

The Quiz Project separates responsibilities into functions instead of putting all logic into one large block.

Example:

```js
function disableButton(button) {
  button.disabled = true;
}
```

The important quiz function `isCorrect(guess)` checks whether the user's guess matches the correct answer.

```js
function isCorrect(guess) {
  return guess === fact.answer;
}
```

It receives a guess and returns a Boolean:

```text
true  → correct
false → incorrect
```

Example use:

```js
if (isCorrect(guess)) {
  console.log("Correct!");
} else {
  console.log("Incorrect!");
}
```

The Day 2 material also covers Boolean conversion and `toString()`:

```js
const answer = true;
console.log(answer.toString()); // "true"
```

---

# 6. Scope

**Scope** determines where a variable can be accessed.

Outer variables can be accessible inside nested functions:

```js
const name = "Reem";

function greet() {
  console.log(name);
}

greet();
```

A variable declared inside a function belongs to that function's scope:

```js
function greet() {
  const message = "Hello";
  console.log(message);
}
```

This will not normally work:

```js
function greet() {
  const message = "Hello";
}

console.log(message);
```

because `message` is not available outside the function.

---

# 7. `let` vs `var`

`let` is **block-scoped**:

```js
if (true) {
  let message = "Hello";
  console.log(message);
}
```

The variable belongs to the `{ }` block.

`var` is **function-scoped**:

```js
function example() {
  var message = "Hello";
  console.log(message);
}
```

| Keyword | Scope |
|---|---|
| `let` | Block scope |
| `var` | Function scope |

Modern JavaScript generally prefers `let` and `const` for predictable block scoping.

---

# 8. Events and Event Handlers

JavaScript can respond to browser/user events such as `click`, `mouseover`, and `mouseout`.

The main method is `addEventListener()`:

```js
const button = document.querySelector("#submit-btn");

button.addEventListener("click", function () {
  console.log("Button clicked!");
});
```

The listener contains an **event type** and a **handler function**.

### Click

```js
button.addEventListener("click", function () {
  console.log("Clicked");
});
```

### Mouseover

```js
button.addEventListener("mouseover", function () {
  console.log("Mouse is over the button");
});
```

### Mouseout

```js
button.addEventListener("mouseout", function () {
  console.log("Mouse left the button");
});
```

---

# 9. Event Object

An event handler can receive an **event object** containing information about the event.

```js
button.addEventListener("click", function (event) {
  console.log(event);
});
```

In the Quiz Project, the event object can be used to identify the element that was clicked and therefore the selected answer.

---

# 10. Conditionals

Conditionals allow JavaScript to make decisions.

```js
const score = 8;

if (score >= 5) {
  console.log("You passed!");
} else {
  console.log("Try again!");
}
```

Quiz example:

```js
if (isCorrect(guess)) {
  console.log("Correct answer!");
} else {
  console.log("Incorrect answer!");
}
```

---

# 11. Truthy and Falsy

When JavaScript evaluates a value in a condition, it treats it as truthy or falsy.

Common falsy values include:

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
  console.log("No username");
}
```

A non-empty string is truthy; an empty string is falsy.

---

# 12. Logical Operators

## AND — `&&`

Both conditions must be true:

```js
if (age >= 18 && hasID) {
  console.log("Access allowed");
}
```

## OR — `||`

At least one condition must be true:

```js
if (isStudent || hasDiscount) {
  console.log("Discount available");
}
```

## NOT — `!`

Reverses a Boolean value:

```js
const isCorrect = false;
console.log(!isCorrect); // true
```

---

# 13. Ternary Operator

The ternary operator is a compact conditional expression.

```js
const message = score >= 5
  ? "You passed!"
  : "Try again!";
```

General form:

```js
condition ? valueIfTrue : valueIfFalse
```

Quiz example:

```js
const result = isCorrect(guess)
  ? "Correct!"
  : "Incorrect!";
```

---

# 14. Loops

Loops repeat code efficiently.

## `for` Loop

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

A `for` loop has initialization, condition, and update:

```text
initialization → condition → body → update → condition → ...
```

## `++`

```js
i++;
```

increases `i` by one.

## `+=`

```js
let score = 0;
score += 1;
```

is equivalent to:

```js
score = score + 1;
```

---

# 15. `for...of`

`for...of` iterates through the values of an iterable such as an array.

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

The loop variable represents the current value.

---

# 16. Quiz Project: Loops and Buttons

The Quiz Project has multiple answer buttons. A loop lets us apply the same logic to every button.

## Add Event Handlers to All Buttons

```js
for (const button of buttons) {
  button.addEventListener("click", handleGuess);
}
```

Conceptually:

```text
buttons
   ↓
loop through buttons
   ↓
button 1 → event handler
button 2 → event handler
button 3 → event handler
...
```

## Disable All Buttons

After an answer is processed:

```js
for (const button of buttons) {
  button.disabled = true;
}
```

This prevents another answer from being selected for the same question.

---

# 17. `isCorrect(guess)`

`isCorrect(guess)` is responsible for checking the user's answer.

Simplified example:

```js
function isCorrect(guess) {
  return guess === fact.answer;
}
```

If:

```js
const fact = { answer: "true" };
const guess = "true";
```

then:

```js
isCorrect(guess); // true
```

If:

```js
const guess = "false";
```

then:

```js
isCorrect(guess); // false
```

The result can control an `if...else` statement:

```js
if (isCorrect(guess)) {
  console.log("Correct!");
} else {
  console.log("Incorrect!");
}
```

---

# 18. Quiz Project: Putting Everything Together

The Quiz Project combines the Day 2 concepts:

- Functions
- Parameters and arguments
- Return values
- Scope
- Events and event handlers
- Event object
- Conditionals
- Truthy/Falsy
- Logical operators
- Loops
- Quiz buttons
- User guesses
- Correct/incorrect state

## Overall Flow

```text
Question displayed
       ↓
Answer buttons available
       ↓
User clicks an answer
       ↓
Event handler runs
       ↓
Get user's guess
       ↓
isCorrect(guess)
       ↓
Compare with correct answer
       ↓
   ┌───┴───┐
Correct  Incorrect
   ↓         ↓
correct   incorrect
state       state
   └───┬─────┘
       ↓
Disable buttons
```

## Combined Example

```js
function isCorrect(guess) {
  return guess === fact.answer;
}

function handleGuess(event) {
  const guess = event.target.textContent;

  if (isCorrect(guess)) {
    event.target.classList.add("correct");
  } else {
    event.target.classList.add("incorrect");
  }

  for (const button of buttons) {
    button.disabled = true;
  }
}

for (const button of buttons) {
  button.addEventListener("click", handleGuess);
}
```

This example shows the complete relationship:

```text
Function
   ↓
Event Handler
   ↓
User Input
   ↓
Conditional
   ↓
Loop
   ↓
Quiz Result
```

---

# 19. Day 2 Summary

| Topic | Main Idea |
|---|---|
| Functions | Reusable blocks of code |
| Parameters | Inputs defined by a function |
| Arguments | Actual values passed to a function |
| Return | Sends a value back from a function |
| Arrow Functions | Alternative function syntax |
| Scope | Determines variable accessibility |
| `let` | Block-scoped variable |
| `var` | Function-scoped variable |
| Events | User/browser actions |
| `addEventListener()` | Registers an event handler |
| Event Object | Information about an event |
| `if` / `else` | Conditional decisions |
| Truthy/Falsy | How values behave in conditions |
| `&&` | Logical AND |
| `||` | Logical OR |
| `!` | Logical NOT |
| Ternary | Short conditional expression |
| `for` | Repeats code using a counter |
| `for...of` | Iterates through values |
| `++` | Increases a value by one |
| `+=` | Adds to an existing value |
| `isCorrect()` | Checks the quiz answer |
| Quiz Project | Combines the Day 2 concepts |

---

# Practice Checklist

- [ ] I can declare a function.
- [ ] I can call a function.
- [ ] I understand parameters.
- [ ] I understand arguments.
- [ ] I can return a value from a function.
- [ ] I can write an arrow function.
- [ ] I understand JavaScript scope.
- [ ] I understand `let` vs `var`.
- [ ] I can use `addEventListener()`.
- [ ] I understand event handlers.
- [ ] I understand the event object.
- [ ] I can use `if` and `else`.
- [ ] I understand truthy and falsy values.
- [ ] I can use `&&`, `||`, and `!`.
- [ ] I can use the ternary operator.
- [ ] I can write a `for` loop.
- [ ] I can use `for...of`.
- [ ] I understand `++` and `+=`.
- [ ] I can loop through quiz buttons.
- [ ] I can add event handlers using a loop.
- [ ] I can disable buttons using a loop.
- [ ] I understand `isCorrect(guess)`.
- [ ] I can combine functions, events, conditionals, and loops in the Quiz Project.

---

# Day 2 Mental Model

```text
FUNCTIONS
    ↓
Reusable logic
    ↓
SCOPE
    ↓
Variable accessibility
    ↓
EVENTS
    ↓
React to user actions
    ↓
CONDITIONALS
    ↓
Make decisions
    ↓
LOOPS
    ↓
Repeat operations
    ↓
QUIZ PROJECT
    ↓
Combine everything
```

