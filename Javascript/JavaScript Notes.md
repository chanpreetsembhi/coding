## Table of Contents

1. [[#1. Variables|Variables]]
2. [[#2. Data Types|Data Types]]
3. [[#3. Operators|Operators]]
4. [[#4. Conditional Statements|Conditional Statements]]
5. [[#5. Loops|Loops]]
6. [[#6. Functions|Functions]]
7. [[#7. Strings|Strings]]
8. [[#8. Arrays — Basics|Arrays — Basics]]
9. [[#9. forEach()|forEach()]]
10. [[#10. map()|map()]]
11. [[#11. filter()|filter()]]
12. [[#12. reduce()|reduce()]]
13. [[#13. find()|find()]]
14. [[#14. includes()|includes()]]
15. [[#15. sort()|sort()]]
16. [[#16. some() / every()|some() / every()]]
17. [[#17. Objects|Objects]]
18. [[#18. Template Literals|Template Literals]]
19. [[#19. Destructuring|Destructuring]]
20. [[#20. Spread / Rest Operator|Spread / Rest Operator]]
21. [[#21. Ternary Operator|Ternary Operator]]
22. [[#22. Default Parameters|Default Parameters]]
23. [[#23. Optional Chaining|Optional Chaining]]
24. [[#24. DOM Manipulation|DOM Manipulation]]
25. [[#25. Event Handling|Event Handling]]
26. [[#26. Promises|Promises]]
27. [[#27. async/await|async/await]]
28. [[#28. fetch()|fetch()]]
29. [[#29. Error Handling|Error Handling]]

---

## 1. Variables

Used to store data.

**Syntax:**

```javascript
var x = 10;    // old way, avoid
let y = 20;    // can change value
const z = 30;  // cannot change value
```

**Example:**

```javascript
let age = 21;
age = 22; // allowed

const name = "Aman";
// name = "Riya"; // Error - can't reassign const
```

[[#Table of Contents |⬆ Back to top]]

---

## 2. Data Types

**Syntax / types:**

```javascript
let str = "Hello";        // String
let num = 25;              // Number
let isTrue = true;         // Boolean
let empty = null;          // Null
let notDefined;             // Undefined
let big = 123n;            // BigInt
let sym = Symbol("id");    // Symbol
let obj = { name: "Riya" };   // Object
let arr = [1, 2, 3];          // Array
```

**Example:**

```javascript
console.log(typeof "Hello"); // string
console.log(typeof 25);      // number
console.log(typeof true);    // boolean
console.log(typeof obj);     // object
```

[[#Table of Contents |⬆ Back to top]]

---

## 3. Operators

**Syntax:**

```javascript
// Arithmetic: + - * / % **
// Comparison: == === != !==
// Logical: && || !
```

**Example:**

```javascript
console.log(5 + 3);     // 8
console.log(5 % 3);     // 2
console.log(5 ** 2);    // 25
console.log(5 == "5");  // true  (loose)
console.log(5 === "5"); // false (strict)
console.log(true && false); // false
```

[[#Table of Contents |⬆ Back to top]]

---

## 4. Conditional Statements

**Syntax:**

```javascript
if (condition) {
  // code
} else if (condition2) {
  // code
} else {
  // code
}
```

**Example:**

```javascript
let marks = 75;

if (marks >= 90) {
  console.log("Grade A");
} else if (marks >= 60) {
  console.log("Grade B");
} else {
  console.log("Grade C");
}
// Output: Grade B
```

**switch syntax:**

```javascript
switch (value) {
  case option1:
    // code
    break;
  default:
    // code
}
```

**Example:**

```javascript
let day = 2;
switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  default:
    console.log("Invalid day");
}
// Output: Tuesday
```

[[#Table of Contents |⬆ Back to top]]

---

## 5. Loops

**Syntax:**

```javascript
for (let i = 0; i < 5; i++) { }
while (condition) { }
do { } while (condition);
for (const item of array) { }
for (const key in object) { }
```

**Example:**

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
// Output: 1 2 3 4 5

const fruits = ["apple", "banana", "mango"];
for (const fruit of fruits) {
  console.log(fruit);
}
```

[[#Table of Contents |⬆ Back to top]]

---

## 6. Functions

**Syntax:**

```javascript
function name(params) { return value; }
const name = function(params) { return value; };
const name = (params) => value;
```

**Example:**

```javascript
function greet(name) {
  return `Hello, ${name}`;
}
console.log(greet("Riya"));
// Output: Hello, Riya

const greetArrow = (name) => `Hello, ${name}`;
console.log(greetArrow("Karan"));
// Output: Hello, Karan
```

[[#Table of Contents |⬆ Back to top]]

---

## 7. Strings

**Syntax:**

```javascript
str.length
str.toUpperCase()
str.toLowerCase()
str.slice(start, end)
str.includes(value)
str.replace(old, new)
str.split(separator)
str.trim()
```

**Example:**

```javascript
let str = "Hello World";

console.log(str.toUpperCase());       // "HELLO WORLD"
console.log(str.slice(0, 5));         // "Hello"
console.log(str.includes("World"));   // true
console.log(str.split(" "));          // ["Hello", "World"]
```

[[#Table of Contents |⬆ Back to top]]

---

## 8. Arrays — Basics

**Syntax:**

```javascript
arr.push(value)     // add at end
arr.pop()           // remove from end
arr.unshift(value)  // add at start
arr.shift()         // remove from start
arr.length
arr.indexOf(value)
arr.reverse()
arr.join(separator)
```

**Example:**

```javascript
let arr = [1, 2, 3];

arr.push(4);     // [1,2,3,4]
arr.pop();       // [1,2,3]
arr.unshift(0);  // [0,1,2,3]
arr.shift();     // [1,2,3]

console.log(arr.join(", "));
// Output: "1, 2, 3"
```

[[#Table of Contents |⬆ Back to top]]

---

## 9. forEach()

Loops through each element, runs a function. Doesn't return a new array.

**Syntax:**

```javascript
array.forEach(function(element) {
  // code
});
```

**Example:**

```javascript
const fruits = ["apple", "banana", "mango"];

fruits.forEach(fruit => console.log(fruit));
// Output:
// apple
// banana
// mango
```

[[#Table of Contents |⬆ Back to top]]

---

## 10. map()

Transforms each element and **returns a new array**.

**Syntax:**

```javascript
const newArray = array.map(item => transformedItem);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(num => num * 2);

console.log(doubled);
// Output: [2, 4, 6, 8]
```

[[#Table of Contents |⬆ Back to top]]

---

## 11. filter()

Keeps elements that pass a test, **returns a new array**.

**Syntax:**

```javascript
const newArray = array.filter(item => condition);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evens = numbers.filter(num => num % 2 === 0);

console.log(evens);
// Output: [2, 4, 6]
```

[[#Table of Contents |⬆ Back to top]]

---

## 12. reduce()

Combines all array elements into a single value.

**Syntax:**

```javascript
array.reduce(function(acc, current) {
  return updatedAcc;
}, initialValue);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((acc, num) => acc + num, 0);

console.log(sum);
// Output: 10
```

[[#Table of Contents |⬆ Back to top]]

---

## 13. find()

Returns the first element matching a condition.

**Syntax:**

```javascript
array.find(item => condition);
```

**Example:**

```javascript
const numbers = [5, 12, 8, 130, 44];

const found = numbers.find(num => num > 10);

console.log(found);
// Output: 12
```

[[#Table of Contents |⬆ Back to top]]

---

## 14. includes()

Checks if array contains a value. Returns true/false.

**Syntax:**

```javascript
array.includes(value);
```

**Example:**

```javascript
const fruits = ["apple", "banana", "mango"];

console.log(fruits.includes("banana"));
// Output: true
```

[[#Table of Contents |⬆ Back to top]]

---

## 15. sort()

Sorts array elements in place.

**Syntax:**

```javascript
array.sort((a, b) => a - b); // ascending
```

**Example:**

```javascript
const numbers = [40, 100, 1, 5, 25];

numbers.sort((a, b) => a - b);

console.log(numbers);
// Output: [1, 5, 25, 40, 100]
```

[[#Table of Contents |⬆ Back to top]]

---

## 16. some() / every()

`some()` — true if at least one passes. `every()` — true only if all pass.

**Syntax:**

```javascript
array.some(item => condition);
array.every(item => condition);
```

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.some(num => num > 4));
// Output: true

console.log(numbers.every(num => num > 0));
// Output: true
```

[[#Table of Contents |⬆ Back to top]]

---

## 17. Objects

**Syntax:**

```javascript
const obj = {
  key: value,
  method: function() { }
};
obj.key;
obj.key = newValue;
delete obj.key;
```

**Example:**

```javascript
const person = {
  name: "Simran",
  age: 23,
  greet: function() {
    console.log(`Hi, I am ${this.name}`);
  }
};

console.log(person.name);   // Simran
person.greet();             // Hi, I am Simran
```

[[#Table of Contents |⬆ Back to top]]

---

## 18. Template Literals

Insert variables directly into strings using backticks.

**Syntax:**

```javascript
`text ${variable} text`
```

**Example:**

```javascript
const name = "Riya";
console.log(`My name is ${name}.`);
// Output: My name is Riya.
```

[[#Table of Contents |⬆ Back to top]]

---

## 19. Destructuring

Extract values from objects/arrays into variables.

**Syntax:**

```javascript
const { key1, key2 } = object;
const [item1, item2] = array;
```

**Example:**

```javascript
const person = { name: "Aman", age: 25 };
const { name, age } = person;

console.log(name, age);
// Output: Aman 25
```

[[#Table of Contents |⬆ Back to top]]

---

## 20. Spread / Rest Operator

`...` expands or collects values.

**Syntax:**

```javascript
const newArr = [...arr1, ...arr2]; // spread
function sum(...nums) { }          // rest
```

**Example:**

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5];
console.log([...arr1, ...arr2]);
// Output: [1, 2, 3, 4, 5]

function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
console.log(sum(1, 2, 3));
// Output: 6
```

[[#Table of Contents |⬆ Back to top]]

---

## 21. Ternary Operator

Short one-line if/else.

**Syntax:**

```javascript
condition ? valueIfTrue : valueIfFalse;
```

**Example:**

```javascript
const age = 18;
const result = age >= 18 ? "Adult" : "Minor";

console.log(result);
// Output: Adult
```

[[#Table of Contents |⬆ Back to top]]

---

## 22. Default Parameters

Set a default value if no argument is passed.

**Syntax:**

```javascript
function greet(name = "Guest") { }
```

**Example:**

```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet();
// Output: Hello, Guest!
```

[[#Table of Contents |⬆ Back to top]]

---

## 23. Optional Chaining

Safely access nested properties without errors.

**Syntax:**

```javascript
object?.property?.nestedProperty;
```

**Example:**

```javascript
const user = { name: "Neha" };

console.log(user?.address?.city);
// Output: undefined (no error)
```

[[#Table of Contents |⬆ Back to top]]

---

## 24. DOM Manipulation

**Syntax:**

```javascript
document.getElementById("id");
document.querySelector(".class");
document.querySelectorAll(".class");

element.textContent = "text";
element.innerHTML = "<b>bold</b>";
element.style.color = "blue";
element.classList.add("active");
element.classList.remove("active");
element.classList.toggle("active");

const el = document.createElement("p");
document.body.appendChild(el);
element.remove();
```

**Example:**

```javascript
const title = document.querySelector("#title");
title.textContent = "New Text";
title.style.color = "blue";
title.classList.add("active");

const newPara = document.createElement("p");
newPara.textContent = "I am new!";
document.body.appendChild(newPara);
```

[[#Table of Contents |⬆ Back to top]]

---

## 25. Event Handling

**Syntax:**

```javascript
element.addEventListener("event", function(e) {
  // code
});
```

**Example:**

```javascript
const button = document.querySelector("#myButton");

button.addEventListener("click", function() {
  console.log("Button clicked!");
});

const form = document.querySelector("#myForm");
form.addEventListener("submit", function(e) {
  e.preventDefault();
  console.log("Form submitted!");
});
```

[[#Table of Contents |⬆ Back to top]]

---

## 26. Promises

Represents a value available now, later, or never.

**Syntax:**

```javascript
const promise = new Promise(function(resolve, reject) {
  resolve(value); // or reject(error)
});

promise.then(result => { }).catch(error => { });
```

**Example:**

```javascript
const promise = new Promise((resolve, reject) => {
  let success = true;
  success ? resolve("Task completed!") : reject("Task failed.");
});

promise
  .then(result => console.log(result))
  .catch(error => console.log(error));
// Output: Task completed!
```

[[#Table of Contents |⬆ Back to top]]

---

## 27. async/await

Cleaner way to work with promises.

**Syntax:**

```javascript
async function name() {
  const result = await promise;
}
```

**Example:**

```javascript
function getData() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Data received"), 1000);
  });
}

async function fetchData() {
  console.log("Fetching...");
  const data = await getData();
  console.log(data);
}

fetchData();
// Output:
// Fetching...
// Data received (after 1 sec)
```

[[#Table of Contents |⬆ Back to top]]

---

## 28. fetch()

Used to make API calls (get data from a server).

**Syntax:**

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => { });
```

**Example:**

```javascript
async function getUsers() {
  const response = await fetch("https://api.example.com/users");
  const data = await response.json();
  console.log(data);
}
```

[[#Table of Contents |⬆ Back to top]]

---

## 29. Error Handling

**Syntax:**

```javascript
try {
  // risky code
} catch (error) {
  // handle error
} finally {
  // always runs
}
```

**Example:**

```javascript
try {
  let result = riskyFunction();
} catch (error) {
  console.log("Something went wrong:", error.message);
} finally {
  console.log("This always runs");
}
```

[[#Table of Contents |⬆ Back to top]]

---

## Quick order to learn (recommended)

1. Variables → Data types → Operators
2. Conditionals → Loops
3. Functions → Strings → Arrays basics
4. forEach → map → filter → reduce → find → includes → sort → some/every
5. Objects → Template literals → Destructuring → Spread/rest
6. Ternary → Default parameters → Optional chaining
7. DOM manipulation → Event handling
8. Promises → async/await → fetch
9. Error handling