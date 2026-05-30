# JavaScript Fundamentals

## What I Learned

JavaScript is one of the most important programming languages because it powers:
- Frontend applications
- Backend services (Node.js)
- APIs
- Modern web applications

---

# 1. What is JavaScript?

JavaScript is a programming language used to make web pages interactive.

Used for:
- Frontend Development (React, Angular, Vue)
- Backend Development (Node.js)
- APIs
- Full Stack Development

Example:

```javascript
console.log("Hello World");
```

---

# 2. Variables

## var

```javascript
var name = "John";
```

Characteristics:
- Function scoped
- Can be redeclared
- Can be reassigned

```javascript
var x = 10;
var x = 20; // allowed
```

Not recommended in modern JavaScript.

---

## let

```javascript
let age = 25;
```

Characteristics:
- Block scoped
- Can be reassigned
- Cannot be redeclared

```javascript
let age = 25;
age = 30;
```

---

## const

```javascript
const PI = 3.14;
```

Characteristics:
- Block scoped
- Cannot be reassigned
- Preferred by default

```javascript
const PI = 3.14;
```

---

### Interview Answer

> Use `const` by default, `let` when values change, and avoid `var`.

---

# 3. Data Types

## Primitive Types

- Number
- String
- Boolean
- Null
- Undefined
- Symbol
- BigInt

Example:

```javascript
let age = 25;
let name = "Varshini";
let isActive = true;
```

---

## Non-Primitive Types

- Object
- Array
- Function

Example:

```javascript
let person = {
  name: "Varshini",
  age: 24
};
```

---

# 4. == vs ===

## == (Loose Equality)

Checks only values.

```javascript
5 == "5"
```

Result:

```javascript
true
```

---

## === (Strict Equality)

Checks:
- value
- datatype

```javascript
5 === "5"
```

Result:

```javascript
false
```

---

### Interview Answer

> Always prefer `===` because it avoids unexpected type conversions.

---

# 5. Functions

## Normal Function

```javascript
function add(a, b) {
  return a + b;
}
```

---

## Arrow Function

```javascript
const add = (a, b) => a + b;
```

Commonly used in:
- React
- Modern JavaScript

---

# 6. Arrays

```javascript
let nums = [1, 2, 3, 4];
```

Important methods:

- push()
- pop()
- shift()
- unshift()
- map()
- filter()
- reduce()

Example:

```javascript
nums.push(5);
```

Adds element at end.

---

# 7. Objects

```javascript
const user = {
  name: "Varshini",
  age: 24
};
```

Access values:

```javascript
user.name
user["name"]
```

---

# 8. forEach vs map

## forEach()

Used for iteration.

```javascript
arr.forEach(item => console.log(item));
```

Returns:

```javascript
undefined
```

---

## map()

Used for transformation.

```javascript
let doubled = arr.map(x => x * 2);
```

Returns:

```javascript
new array
```

---

### Interview Favorite

> forEach = iterate  
> map = transform and return new array

---

# 9. filter()

Returns matching elements.

```javascript
let even = arr.filter(x => x % 2 === 0);
```

Output:

```javascript
[2,4,6]
```

---

# 10. reduce()

Converts array into a single value.

```javascript
let sum = arr.reduce((a, b) => a + b, 0);
```

Output:

```javascript
10
```

---

# 11. Scope

## Global Scope

Accessible everywhere.

```javascript
let x = 10;
```

---

## Function Scope

```javascript
function test() {
  let y = 20;
}
```

Accessible only inside function.

---

## Block Scope

```javascript
if (true) {
  let z = 30;
}
```

Accessible only inside block.

---

# 12. Hoisting

JavaScript moves declarations to the top.

Example:

```javascript
console.log(x);

var x = 10;
```

Output:

```javascript
undefined
```

Equivalent to:

```javascript
var x;

console.log(x);

x = 10;
```

---

# 13. Closures

A function remembers variables from its outer scope.

```javascript
function outer() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}
```

Common Uses:
- Counters
- Private Variables
- Callbacks

---

# 14. Callback Functions

Function passed as an argument to another function.

```javascript
function greet(name, callback) {
  callback();
}
```

Used heavily in:
- Async programming
- Event handling

---

# 15. Promises

Used to handle asynchronous operations.

States:
- Pending
- Fulfilled (Resolved)
- Rejected

Example:

```javascript
fetch(url)
  .then(data => console.log(data))
  .catch(err => console.log(err));
```

---

# 16. Async / Await

Cleaner way to handle promises.

```javascript
async function getData() {
  const response = await fetch(url);
  return response;
}
```

### Interview Answer

> Async/Await is built on top of Promises and makes asynchronous code easier to read.

---

# 17. Event Loop

JavaScript is:

> Single Threaded

Yet it handles async operations using:

- Call Stack
- Web APIs
- Callback Queue
- Event Loop

---

### Interview Answer

Browser handles async work through Web APIs.

When completed:
- callback enters queue
- Event Loop pushes callback into Call Stack

---

# 18. setTimeout()

```javascript
setTimeout(() => {
  console.log("Hello");
}, 2000);
```

Runs after approximately 2 seconds.

---

# 19. DOM

DOM stands for:

> Document Object Model

Allows JavaScript to interact with HTML.

Examples:

```javascript
document.getElementById("title");
document.querySelector(".box");
```

---

# 20. this Keyword

Refers to the current object.

```javascript
const user = {
  name: "Varshini",

  greet() {
    console.log(this.name);
  }
};
```

Output:

```javascript
Varshini
```

---

# 21. Spread Operator (...)

Used to copy arrays and objects.

```javascript
let arr2 = [...arr1];

let user2 = { ...user1 };
```

---

# 22. Destructuring

Extract values easily.

Array:

```javascript
const [a, b] = [10, 20];
```

Object:

```javascript
const { name, age } = user;
```

---

# 23. Template Literals

Used for string interpolation.

```javascript
let name = "Varshini";

console.log(`Hello ${name}`);
```

---

# 24. Null vs Undefined

## Undefined

Variable declared but not assigned.

```javascript
let x;
```

---

## Null

Intentional empty value.

```javascript
let x = null;
```

