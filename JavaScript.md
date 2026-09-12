## Different data types in JavaScript.
- There are 8 data types in JavaScript. 7 are primitive data types, and 1 is object data type.
- Number : A number representing a numeric value
- Bigint : A number representing a large integer
- String : A text of characters enclosed in quotes
- Boolean :	A data type representing true or false
- Undefined	: A variable with no assigned value
- Null	: A value representing object absence
- Symbol	: A unique primitive identifier
- Object	: A collection of key-value pairs of data

## scopes in javaScript.
- Scope means the accessibility of variables.
- There are 3 types of scope: Global scope, Function scope, and block scope.
- Variables declared globally (outside any block or function) have Global Scope, and global variables can be accessed from anywhere in a JavaScript program.
- Function scope: Variables defined inside a function are not accessible from outside the function.
- Variables declared with let and const inside a code block are "block-scoped," meaning they are only accessible within that block.

## let, var, const
- let is used to declare variables with block scope. Its value can be changed later.
- const is used to declare variables with block scope. The variable cannot be reassigned after initialization.
- var is function-scoped, not global-scoped. If declared outside a function, it becomes global-scoped.

## Why we must not use var.
- Because var is not block-scoped, and it can be redeclared.
## Why is using global variables bad?
- Because any part of the program can access and modify them, which can cause readability, maintainability, debugging, and name-collision issues.
## Truthy and falsy values.
- In javaScript truthy and falsy values means what happened to vaiables when they treated as boolean.
- Truthy values: "hello", "0", [], {}, 42, -10, true
- Falsy values: false, 0, -0, 0n, "", null, undefined, NaN

## Function hoisting
- In JavaScript, function hoisting refers to calling a function before its declaration.

## what happens when a function does not have a return statement
- its return undefined.

## different ways of declaring a function
```javascript
### Function Declaration


function add(a, b) {
    return a + b;
}

console.log(add(2, 3));


### 2. Function Expression

```md
# Function Expression

```javascript
const add = function(a, b) {
    return a + b;
};

console.log(add(2, 3));


### 3. Arrow Function

```md
# Arrow Function

```javascript
const add = (a, b) => {
    return a + b;
};

console.log(add(2, 3));


### 4. Short Arrow Function

```md
# Short Arrow Function

```javascript
const add = (a, b) => a + b;

console.log(add(2, 3));


### 5. Named Function Expression

```md
# Named Function Expression

```javascript
const add = function addition(a, b) {
    return a + b;
};

console.log(add(2, 3))

```


## different types of for loops - for with numbers, for..in, for..of, forEach, while
### `for` Loop with Numbers
```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```
### `for...in` Loop
```javascript
const person = {
    name: 'Aniket',
    age: 32,
    city: 'Bangalore'
};

for (const key in person) {
    console.log(key);
}
```
### `for...of` Loop
```javascript
const fruits = ['Apple', 'Banana', 'Mango'];

for (const fruit of fruits) {
    console.log(fruit);
}
```
### `forEach()` Loop
```javascript
const fruits = ['Apple', 'Banana', 'Mango'];

fruits.forEach(function (fruit) {
    console.log(fruit);
});
```

### `while` Loop
```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
    i++;
}
```

# Popular Array Utility Methods in JavaScript

JavaScript arrays provide many built-in methods for adding, removing, combining, searching, and manipulating elements.

## Mutable vs Immutable

- **Mutable method** → changes the original array.
- **Immutable method** → does not change the original array and returns a new value/array.

---

# Basics

## 1. `Array.pop()`

Removes the **last element** from an array.

**Mutable:** Yes

### Example

```javascript
const numbers = [10, 20, 30];

const result = numbers.pop();

console.log(result);
console.log(numbers);
```

Output:

```text
30
[10, 20]
```

`pop()` changes the original array.

---

## 2. `Array.push()`

Adds one or more elements to the **end** of an array.

**Mutable:** Yes

### Example

```javascript
const numbers = [10, 20];

const result = numbers.push(30);

console.log(result);
console.log(numbers);
```

Output:

```text
3
[10, 20, 30]
```

`push()` returns the **new length** of the array.

---

## 3. `Array.concat()`

Combines two or more arrays and returns a **new array**.

**Mutable:** No

### Example

```javascript
const numbers1 = [10, 20];
const numbers2 = [30, 40];

const result = numbers1.concat(numbers2);

console.log(result);
console.log(numbers1);
```

Output:

```text
[10, 20, 30, 40]
[10, 20]
```

The original arrays are not changed.

---

## 4. `Array.slice()`

Returns a portion of an array as a **new array**.

**Mutable:** No

### Syntax

```javascript
array.slice(start, end);
```

The `end` index is **not included**.

### Example

```javascript
const numbers = [10, 20, 30, 40, 50];

const result = numbers.slice(1, 4);

console.log(result);
console.log(numbers);
```

Output:

```text
[20, 30, 40]
[10, 20, 30, 40, 50]
```

The original array remains unchanged.

---

## 5. `Array.splice()`

Adds, removes, or replaces elements in an array.

**Mutable:** Yes

### Example: Remove elements

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.splice(1, 2);

console.log(result);
console.log(numbers);
```

Output:

```text
[20, 30]
[10, 40]
```

Here:

```javascript
numbers.splice(1, 2);
```

means:

- Start at index `1`
- Remove `2` elements

### Example: Add elements

```javascript
const numbers = [10, 20, 40];

numbers.splice(2, 0, 30);

console.log(numbers);
```

Output:

```text
[10, 20, 30, 40]
```

---

## 6. `Array.join()`

Combines all array elements into a **string** using a separator.

**Mutable:** No

### Example

```javascript
const fruits = ['Apple', 'Banana', 'Mango'];

const result = fruits.join(', ');

console.log(result);
console.log(fruits);
```

Output:

```text
Apple, Banana, Mango
['Apple', 'Banana', 'Mango']
```

The original array is not changed.

### Example with another separator

```javascript
const words = ['JavaScript', 'is', 'easy'];

console.log(words.join(' '));
```

Output:

```text
JavaScript is easy
```

---

## 7. `Array.flat()`

Creates a new array by flattening nested arrays.

**Mutable:** No

### Example

```javascript
const numbers = [1, 2, [3, 4], [5, 6]];

const result = numbers.flat();

console.log(result);
console.log(numbers);
```

Output:

```text
[1, 2, 3, 4, 5, 6]
[1, 2, [3, 4], [5, 6]]
```

The original array is unchanged.

### Nested arrays

```javascript
const numbers = [1, [2, [3, [4]]]];

console.log(numbers.flat());
```

Output:

```text
[1, 2, [3, [4]]]
```

By default, `flat()` only flattens **one level**.

To flatten more levels:

```javascript
console.log(numbers.flat(Infinity));
```

Output:

```text
[1, 2, 3, 4]
```

---

# Finding Methods

## 8. `Array.find()`

Returns the **first element** that satisfies a condition.

**Mutable:** No

### Example

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.find((number) => number > 25);

console.log(result);
```

Output:

```text
30
```

The method stops after finding the first matching element.

### If no element is found

```javascript
const numbers = [10, 20, 30];

const result = numbers.find((number) => number > 50);

console.log(result);
```

Output:

```text
undefined
```

---

## 9. `Array.indexOf()`

Returns the **index of the first occurrence** of a value.

**Mutable:** No

### Example

```javascript
const numbers = [10, 20, 30, 20];

const result = numbers.indexOf(20);

console.log(result);
```

Output:

```text
1
```

### Value not found

```javascript
const numbers = [10, 20, 30];

console.log(numbers.indexOf(50));
```

Output:

```text
-1
```

---

## 10. `Array.includes()`

Checks whether an array contains a particular value.

Returns `true` or `false`.

**Mutable:** No

### Example

```javascript
const fruits = ['Apple', 'Banana', 'Mango'];

console.log(fruits.includes('Banana'));
```

Output:

```text
true
```

### Value not found

```javascript
console.log(fruits.includes('Orange'));
```

Output:

```text
false
```

---

## 11. `Array.findIndex()`

Returns the **index of the first element** that satisfies a condition.

**Mutable:** No

### Example

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.findIndex((number) => number > 25);

console.log(result);
```

Output:

```text
2
```

The element at index `2` is `30`.

### If no element is found

```javascript
const numbers = [10, 20, 30];

const result = numbers.findIndex((number) => number > 50);

console.log(result);
```

Output:

```text
-1
```

---

# Quick Comparison

| Method | Purpose | Mutable? | Return Value |
|---|---|---:|---|
| `pop()` | Remove last element | Yes | Removed element |
| `push()` | Add element at end | Yes | New array length |
| `concat()` | Combine arrays | No | New array |
| `slice()` | Extract part of array | No | New array |
| `splice()` | Add/remove/replace elements | Yes | Removed elements |
| `join()` | Convert array to string | No | String |
| `flat()` | Flatten nested arrays | No | New array |
| `find()` | Find first matching value | No | Element / `undefined` |
| `indexOf()` | Find index of a value | No | Index / `-1` |
| `includes()` | Check if value exists | No | `true` / `false` |
| `findIndex()` | Find index using condition | No | Index / `-1` |

---

# Mutable vs Immutable Summary

## Mutable Methods

These methods **change the original array**:

```text
pop()
push()
splice()
```

Example:

```javascript
const numbers = [10, 20, 30];

numbers.push(40);

console.log(numbers);
```

Output:

```text
[10, 20, 30, 40]
```

The original array has changed.

---

## Immutable Methods

These methods **do not change the original array**:

```text
concat()
slice()
join()
flat()
find()
indexOf()
includes()
findIndex()
```

Example:

```javascript
const numbers = [10, 20, 30];

const result = numbers.slice(0, 2);

console.log(result);
console.log(numbers);
```

Output:

```text
[10, 20]
[10, 20, 30]
```

The original array remains unchanged.

---

# Important Difference: `slice()` vs `splice()`

This is a common interview question.

### `slice()`

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.slice(1, 3);

console.log(result);
console.log(numbers);
```

Output:

```text
[20, 30]
[10, 20, 30, 40]
```

**`slice()` does not modify the original array.**

### `splice()`

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.splice(1, 2);

console.log(result);
console.log(numbers);
```

Output:

```text
[20, 30]
[10, 40]
```

**`splice()` modifies the original array.**

### Remember

```text
slice  → immutable → returns a portion
splice → mutable   → adds/removes/replaces
```

# Higher Order Functions

A **Higher Order Function (HOF)** is a function that does at least one of the following:

- Takes another function as an argument.
- Returns a function.

Array methods such as `forEach()`, `filter()`, `map()`, and `reduce()` are commonly used as higher-order functions because they accept a callback function.

---

# 1. `Array.forEach()`

`forEach()` executes a callback function once for every element in an array.

**Mutable:** No

**Returns:** `undefined`

### Example

```javascript
const numbers = [10, 20, 30];

numbers.forEach((number) => {
    console.log(number);
});
```

Output:

```text
10
20
30
```

### With index

```javascript
const fruits = ['Apple', 'Banana', 'Mango'];

fruits.forEach((fruit, index) => {
    console.log(index, fruit);
});
```

Output:

```text
0 Apple
1 Banana
2 Mango
```

### Important

`forEach()` is mainly used when you want to **perform an action** for every element.

```javascript
const numbers = [1, 2, 3];

const result = numbers.forEach((number) => {
    return number * 2;
});

console.log(result);
```

Output:

```text
undefined
```

`forEach()` does not create a new array.

---

# 2. `Array.filter()`

`filter()` creates a **new array** containing elements that satisfy a condition.

**Mutable:** No

**Returns:** New array

### Example

```javascript
const numbers = [10, 15, 20, 25, 30];

const result = numbers.filter((number) => {
    return number > 20;
});

console.log(result);
```

Output:

```text
[25, 30]
```

### Short version

```javascript
const numbers = [10, 15, 20, 25, 30];

const result = numbers.filter(number => number > 20);

console.log(result);
```

### Filtering even numbers

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

The original array remains unchanged.

---

# 3. `Array.map()`

`map()` creates a **new array** by transforming every element.

**Mutable:** No

**Returns:** New array

### Example

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.map((number) => {
    return number * 2;
});

console.log(result);
```

Output:

```text
[2, 4, 6, 8]
```

The original array is unchanged:

```javascript
console.log(numbers);
```

Output:

```text
[1, 2, 3, 4]
```

### Example with strings

```javascript
const names = ['aniket', 'rahul', 'amit'];

const upperNames = names.map(name => name.toUpperCase());

console.log(upperNames);
```

Output:

```text
['ANIKET', 'RAHUL', 'AMIT']
```

### `map()` vs `forEach()`

`map()` returns a new array:

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(number => number * 2);

console.log(result);
```

Output:

```text
[2, 4, 6]
```

`forEach()` returns `undefined`:

```javascript
const numbers = [1, 2, 3];

const result = numbers.forEach(number => number * 2);

console.log(result);
```

Output:

```text
undefined
```

---

# 4. `Array.reduce()`

`reduce()` processes all elements of an array and combines them into a **single value**.

**Mutable:** No

**Returns:** A single accumulated value

### Example: Sum of numbers

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);

console.log(result);
```

Output:

```text
100
```

Here:

```javascript
0
```

is the initial value of `sum`.

The calculation happens like this:

```text
0 + 10 = 10
10 + 20 = 30
30 + 30 = 60
60 + 40 = 100
```

### Example: Find the product

```javascript
const numbers = [2, 3, 4];

const result = numbers.reduce((product, number) => {
    return product * number;
}, 1);

console.log(result);
```

Output:

```text
24
```

### Example: Count numbers

```javascript
const numbers = [10, 20, 10, 30, 10];

const result = numbers.reduce((count, number) => {
    if (number === 10) {
        count++;
    }

    return count;
}, 0);

console.log(result);
```

Output:

```text
3
```

---

# 5. `Array.sort()`

`sort()` sorts the elements of an array.

**Mutable:** Yes

**Returns:** The sorted array

### Example

```javascript
const fruits = ['Mango', 'Apple', 'Banana'];

fruits.sort();

console.log(fruits);
```

Output:

```text
['Apple', 'Banana', 'Mango']
```

`sort()` modifies the original array.

---

## Sorting Numbers

By default, `sort()` converts elements to strings and sorts them lexicographically.

Therefore:

```javascript
const numbers = [10, 2, 30, 4];

numbers.sort();

console.log(numbers);
```

Output:

```text
[10, 2, 30, 4]
```

This is not numerical sorting.

### Ascending order

Use a comparison function:

```javascript
const numbers = [10, 2, 30, 4];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output:

```text
[2, 4, 10, 30]
```

### Descending order

```javascript
const numbers = [10, 2, 30, 4];

numbers.sort((a, b) => b - a);

console.log(numbers);
```

Output:

```text
[30, 10, 4, 2]
```

---

# Advanced

# 6. Array Method Chaining

**Method chaining** means calling multiple array methods one after another.

The output of one method becomes the input of the next method.

For example:

```javascript
array
    .filter(...)
    .map(...)
    .reduce(...);
```

---

## Example: `filter()` + `map()`

Suppose we have:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
```

We want to:

1. Select even numbers.
2. Multiply them by 10.

### Without chaining

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(number => number % 2 === 0);

const result = evenNumbers.map(number => number * 10);

console.log(result);
```

Output:

```text
[20, 40, 60]
```

### With chaining

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 10);

console.log(result);
```

Output:

```text
[20, 40, 60]
```

---

## Example: `filter()` + `map()` + `reduce()`

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 10)
    .reduce((sum, number) => sum + number, 0);

console.log(result);
```

Output:

```text
120
```

Step by step:

### Step 1: `filter()`

```javascript
[1, 2, 3, 4, 5, 6]
```

becomes:

```javascript
[2, 4, 6]
```

### Step 2: `map()`

```javascript
[2, 4, 6]
```

becomes:

```javascript
[20, 40, 60]
```

### Step 3: `reduce()`

```javascript
20 + 40 + 60
```

becomes:

```text
120
```

---

# Example with Objects

Consider an array of employees:

```javascript
const employees = [
    { name: 'Aniket', salary: 60000 },
    { name: 'Rahul', salary: 40000 },
    { name: 'Amit', salary: 70000 }
];
```

Find the names of employees whose salary is greater than `50000`.

```javascript
const result = employees
    .filter(employee => employee.salary > 50000)
    .map(employee => employee.name);

console.log(result);
```

Output:

```text
['Aniket', 'Amit']
```

---

# Mutable vs Immutable

| Method | Purpose | Mutable? | Returns |
|---|---|---:|---|
| `forEach()` | Execute code for each element | No | `undefined` |
| `filter()` | Select matching elements | No | New array |
| `map()` | Transform elements | No | New array |
| `reduce()` | Combine elements | No | Single value |
| `sort()` | Sort elements | **Yes** | Sorted array |

---

# Important Differences

## `forEach()`

Use when you want to **perform an action**.

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

## `filter()`

Use when you want to **select elements**.

```javascript
const result = numbers.filter(number => number > 10);
```

## `map()`

Use when you want to **transform elements**.

```javascript
const result = numbers.map(number => number * 2);
```

## `reduce()`

Use when you want to **combine elements into one value**.

```javascript
const result = numbers.reduce((sum, number) => sum + number, 0);
```

## `sort()`

Use when you want to **sort an array**.

```javascript
numbers.sort((a, b) => a - b);
```

---

# Easy Way to Remember

```text
forEach → Do something
filter  → Select something
map     → Transform something
reduce  → Combine something
sort    → Order something
```

### Example

```javascript
const result = numbers
    .filter(...)
    .map(...)
    .reduce(...);
```

Think of it as:

```text
Filter → Map → Reduce
Select → Transform → Combine
```


# Popular String Utility Methods in JavaScript

Strings are sequences of characters used to represent text.

```javascript
const message = "Hello JavaScript";
```

## Mutable vs Immutable

JavaScript strings are **immutable**.

This means once a string is created, its characters cannot be changed directly.

String methods generally return a **new string** instead of modifying the original string.

```javascript
const name = "aniket";

const result = name.toUpperCase();

console.log(result);
console.log(name);
```

Output:

```text
ANIKET
aniket
```

The original string is unchanged.

Therefore, the string methods covered below are **immutable**.

---

# Basics

## 1. `String.toUpperCase()`

Converts a string to uppercase.

**Mutable:** No — Strings are immutable

**Returns:** New string

### Example

```javascript
const message = "hello world";

const result = message.toUpperCase();

console.log(result);
```

Output:

```text
HELLO WORLD
```

The original string remains unchanged:

```javascript
console.log(message);
```

Output:

```text
hello world
```

---

## 2. `String.toLowerCase()`

Converts a string to lowercase.

**Mutable:** No — Strings are immutable

**Returns:** New string

### Example

```javascript
const message = "HELLO WORLD";

const result = message.toLowerCase();

console.log(result);
```

Output:

```text
hello world
```

---

## 3. `String.trim()`

Removes whitespace from the beginning and end of a string.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const message = "   Hello World   ";

const result = message.trim();

console.log(result);
```

Output:

```text
Hello World
```

It does not remove spaces between words.

```javascript
const message = "   Hello   World   ";

console.log(message.trim());
```

Output:

```text
Hello   World
```

---

## 4. `String.trimStart()`

Removes whitespace from the beginning of a string.

**Mutable:** No

### Example

```javascript
const message = "   Hello World   ";

const result = message.trimStart();

console.log(result);
```

Output:

```text
Hello World   
```

---

## 5. `String.trimEnd()`

Removes whitespace from the end of a string.

**Mutable:** No

### Example

```javascript
const message = "   Hello World   ";

const result = message.trimEnd();

console.log(result);
```

Output:

```text
   Hello World
```

---

# Searching

## 6. `String.includes()`

Checks whether a string contains a particular substring.

**Mutable:** No

**Returns:** `true` or `false`

### Example

```javascript
const message = "JavaScript is easy";

console.log(message.includes("JavaScript"));
```

Output:

```text
true
```

### Example

```javascript
console.log(message.includes("Python"));
```

Output:

```text
false
```

`includes()` is case-sensitive.

```javascript
console.log(message.includes("javascript"));
```

Output:

```text
false
```

---

## 7. `String.indexOf()`

Returns the index of the **first occurrence** of a substring.

**Mutable:** No

**Returns:** Index or `-1`

### Example

```javascript
const message = "Hello JavaScript";

const result = message.indexOf("JavaScript");

console.log(result);
```

Output:

```text
6
```

### If not found

```javascript
console.log(message.indexOf("Python"));
```

Output:

```text
-1
```

---

## 8. `String.lastIndexOf()`

Returns the index of the **last occurrence** of a substring.

**Mutable:** No

**Returns:** Index or `-1`

### Example

```javascript
const message = "JavaScript is easy and JavaScript is popular";

const result = message.lastIndexOf("JavaScript");

console.log(result);
```

Output:

```text
25
```

---

## 9. `String.startsWith()`

Checks whether a string starts with a particular substring.

**Mutable:** No

**Returns:** `true` or `false`

### Example

```javascript
const message = "JavaScript is easy";

console.log(message.startsWith("JavaScript"));
```

Output:

```text
true
```

```javascript
console.log(message.startsWith("Python"));
```

Output:

```text
false
```

---

## 10. `String.endsWith()`

Checks whether a string ends with a particular substring.

**Mutable:** No

**Returns:** `true` or `false`

### Example

```javascript
const fileName = "index.js";

console.log(fileName.endsWith(".js"));
```

Output:

```text
true
```

---

# Extracting Parts of a String

## 11. `String.slice()`

Extracts a portion of a string and returns a new string.

**Mutable:** No

**Returns:** New string

### Syntax

```javascript
string.slice(start, end);
```

The `end` index is not included.

### Example

```javascript
const message = "JavaScript";

const result = message.slice(0, 4);

console.log(result);
```

Output:

```text
Java
```

The original string remains unchanged.

```javascript
console.log(message);
```

Output:

```text
JavaScript
```

### Using negative indexes

```javascript
const message = "JavaScript";

console.log(message.slice(-6));
```

Output:

```text
Script
```

---

## 12. `String.substring()`

Extracts characters between two indexes.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const message = "JavaScript";

const result = message.substring(0, 4);

console.log(result);
```

Output:

```text
Java
```

### `slice()` vs `substring()`

```javascript
const message = "JavaScript";

console.log(message.slice(-6));
console.log(message.substring(-6));
```

Output:

```text
Script
JavaScript
```

`substring()` treats negative values as `0`, while `slice()` supports negative indexes.

---

# Replacing

## 13. `String.replace()`

Replaces the first matching substring.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const message = "I like Java";

const result = message.replace("Java", "JavaScript");

console.log(result);
```

Output:

```text
I like JavaScript
```

The original string is unchanged:

```javascript
console.log(message);
```

Output:

```text
I like Java
```

### Replacing the first occurrence

```javascript
const message = "Java is easy. Java is popular.";

const result = message.replace("Java", "JavaScript");

console.log(result);
```

Output:

```text
JavaScript is easy. Java is popular.
```

Only the first occurrence is replaced.

---

## 14. `String.replaceAll()`

Replaces all matching occurrences.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const message = "Java is easy. Java is popular.";

const result = message.replaceAll("Java", "JavaScript");

console.log(result);
```

Output:

```text
JavaScript is easy. JavaScript is popular.
```

---

# Splitting and Joining

## 15. `String.split()`

Splits a string into an array based on a separator.

**Mutable:** No

**Returns:** New array

### Example

```javascript
const message = "JavaScript is easy";

const result = message.split(" ");

console.log(result);
```

Output:

```text
['JavaScript', 'is', 'easy']
```

### Splitting by comma

```javascript
const fruits = "Apple,Banana,Mango";

const result = fruits.split(",");

console.log(result);
```

Output:

```text
['Apple', 'Banana', 'Mango']
```

### Splitting every character

```javascript
const word = "Hello";

console.log(word.split(""));
```

Output:

```text
['H', 'e', 'l', 'l', 'o']
```

---

# Repeating and Padding

## 16. `String.repeat()`

Repeats a string a specified number of times.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const message = "Hi ";

const result = message.repeat(3);

console.log(result);
```

Output:

```text
Hi Hi Hi
```

---

## 17. `String.padStart()`

Adds characters to the beginning of a string until it reaches a specified length.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const number = "123";

const result = number.padStart(5, "0");

console.log(result);
```

Output:

```text
00123
```

---

## 18. `String.padEnd()`

Adds characters to the end of a string until it reaches a specified length.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const number = "123";

const result = number.padEnd(5, "0");

console.log(result);
```

Output:

```text
12300
```

---

# Character Access

## 19. `String.charAt()`

Returns the character at a specified index.

**Mutable:** No

**Returns:** String character

### Example

```javascript
const name = "Aniket";

console.log(name.charAt(0));
```

Output:

```text
A
```

```javascript
console.log(name.charAt(3));
```

Output:

```text
k
```

---

## 20. `String.at()`

Returns the character at a specified index.

It also supports negative indexes.

**Mutable:** No

### Example

```javascript
const name = "Aniket";

console.log(name.at(0));
console.log(name.at(-1));
```

Output:

```text
A
t
```

Negative indexing makes `at()` convenient for accessing characters from the end.

---

# Converting and Formatting

## 21. `String.concat()`

Combines strings and returns a new string.

**Mutable:** No

**Returns:** New string

### Example

```javascript
const firstName = "Aniket";
const lastName = "Kumar";

const result = firstName.concat(" ", lastName);

console.log(result);
```

Output:

```text
Aniket Kumar
```

However, template literals are generally easier to read:

```javascript
const result = `${firstName} ${lastName}`;

console.log(result);
```

---

# Length

## 22. `String.length`

Returns the number of characters in a string.

**Mutable:** No

**Returns:** Number

### Example

```javascript
const name = "Aniket";

console.log(name.length);
```

Output:

```text
6
```

`length` is a property, not a method.

Therefore:

```javascript
name.length
```

is correct, not:

```javascript
name.length()
```

---

# Quick Comparison

| Method / Property | Purpose | Mutable? | Returns |
|---|---|---:|---|
| `toUpperCase()` | Convert to uppercase | No | New string |
| `toLowerCase()` | Convert to lowercase | No | New string |
| `trim()` | Remove whitespace from both ends | No | New string |
| `trimStart()` | Remove beginning whitespace | No | New string |
| `trimEnd()` | Remove ending whitespace | No | New string |
| `includes()` | Check if substring exists | No | Boolean |
| `indexOf()` | Find first occurrence | No | Index / `-1` |
| `lastIndexOf()` | Find last occurrence | No | Index / `-1` |
| `startsWith()` | Check beginning | No | Boolean |
| `endsWith()` | Check ending | No | Boolean |
| `slice()` | Extract part of string | No | New string |
| `substring()` | Extract part of string | No | New string |
| `replace()` | Replace first match | No | New string |
| `replaceAll()` | Replace all matches | No | New string |
| `split()` | Split string into array | No | New array |
| `repeat()` | Repeat string | No | New string |
| `padStart()` | Pad beginning | No | New string |
| `padEnd()` | Pad ending | No | New string |
| `charAt()` | Get character by index | No | String |
| `at()` | Get character by index | No | String |
| `concat()` | Combine strings | No | New string |
| `length` | Get string length | No | Number |

---

# Important Point: Strings Are Immutable

Unlike arrays, strings cannot be changed directly.

For example:

```javascript
let name = "Aniket";

name[0] = "B";

console.log(name);
```

Output:

```text
Aniket
```

The character was not changed.

Instead, create a new string:

```javascript
let name = "Aniket";

name = "B" + name.slice(1);

console.log(name);
```

Output:

```text
Bniket
```

The variable now refers to a new string.

---

# Common String Method Chaining

String methods can also be chained.

### Example

```javascript
const name = "   aniket kumar   ";

const result = name
    .trim()
    .toUpperCase()
    .replace("KUMAR", "SINGH");

console.log(result);
```

Output:

```text
ANIKET SINGH
```

The operations happen from left to right:

```text
"   aniket kumar   "
        ↓ trim()
"aniket kumar"
        ↓ toUpperCase()
"ANIKET KUMAR"
        ↓ replace()
"ANIKET SINGH"
```

---

# Easy Way to Remember

```text
toUpperCase() / toLowerCase() → Change case
trim()                         → Remove outer spaces
includes()                     → Check if present
indexOf()                      → Find position
startsWith() / endsWith()      → Check beginning/end
slice()                        → Extract part
replace() / replaceAll()       → Replace text
split()                        → String → Array
concat()                       → Combine strings
repeat()                       → Repeat text
padStart() / padEnd()          → Add padding
charAt() / at()                → Get character
length                         → Get size
```

## Key Point

```text
JavaScript Strings → Immutable
```

So, string methods do not modify the original string. They return a new string or another value.


# Popular Object Utility Methods in JavaScript

JavaScript provides several built-in methods for working with objects.

> **Important:** Most object utility methods do not modify the original object. They return a new array or value.

---

## 1. Object.keys()

Returns an array containing all the **keys/property names** of an object.

**Immutable:** Yes — does not modify the object.

```javascript
const person = {
    name: 'Aniket',
    age: 32,
    city: 'Mumbai'
};

const keys = Object.keys(person);

console.log(keys);
// ['name', 'age', 'city']

console.log(person);
// Original object is unchanged
```

---

## 2. Object.values()

Returns an array containing all the **values** of an object.

**Immutable:** Yes — does not modify the object.

```javascript
const person = {
    name: 'Aniket',
    age: 32,
    city: 'Mumbai'
};

const values = Object.values(person);

console.log(values);
// ['Aniket', 32, 'Mumbai']
```

---

## 3. Object.entries()

Returns an array containing the object's **key-value pairs**.

Each pair is represented as an array.

**Immutable:** Yes — does not modify the object.

```javascript
const person = {
    name: 'Aniket',
    age: 32,
    city: 'Mumbai'
};

const entries = Object.entries(person);

console.log(entries);

// [
//     ['name', 'Aniket'],
//     ['age', 32],
//     ['city', 'Mumbai']
// ]
```

### Using Object.entries() with for...of

```javascript
for (const [key, value] of Object.entries(person)) {
    console.log(key, value);
}
```

Output:

```text
name Aniket
age 32
city Mumbai
```

---

## 4. Object.fromEntries()

Converts an array of key-value pairs into an object.

**Immutable:** Yes — creates a new object.

```javascript
const entries = [
    ['name', 'Aniket'],
    ['age', 32],
    ['city', 'Mumbai']
];

const person = Object.fromEntries(entries);

console.log(person);

// {
//     name: 'Aniket',
//     age: 32,
//     city: 'Mumbai'
// }
```

---

## 5. Object.assign()

Copies properties from one or more objects into a target object.

**Mutable:** Yes — the target object is modified.

```javascript
const person = {
    name: 'Aniket'
};

const details = {
    age: 32,
    city: 'Mumbai'
};

Object.assign(person, details);

console.log(person);

// {
//     name: 'Aniket',
//     age: 32,
//     city: 'Mumbai'
// }
```

### Important

The first argument is the **target object** and gets modified.

```javascript
Object.assign(target, source);
```

---

## 6. Object.assign() for creating a new object

You can use an empty object as the target to avoid modifying the original object.

**Immutable:** Original object is not modified.

```javascript
const person = {
    name: 'Aniket',
    age: 32
};

const updatedPerson = Object.assign({}, person, {
    city: 'Mumbai'
});

console.log(updatedPerson);

// {
//     name: 'Aniket',
//     age: 32,
//     city: 'Mumbai'
// }

console.log(person);

// {
//     name: 'Aniket',
//     age: 32
// }
```

---

## 7. Object.hasOwn()

Checks whether an object has a specific property as its **own property**.

Returns `true` or `false`.

**Immutable:** Yes — does not modify the object.

```javascript
const person = {
    name: 'Aniket',
    age: 32
};

console.log(Object.hasOwn(person, 'name'));
// true

console.log(Object.hasOwn(person, 'city'));
// false
```

---

## 8. Object.freeze()

Prevents changes to an object.

After freezing, properties cannot be added, removed, or changed.

**Mutable:** No — the object becomes non-modifiable.

```javascript
const person = {
    name: 'Aniket',
    age: 32
};

Object.freeze(person);

person.age = 35;
person.city = 'Mumbai';
delete person.name;

console.log(person);

// {
//     name: 'Aniket',
//     age: 32
// }
```

> `Object.freeze()` itself does not mutate the object's values. Instead, it makes the object immutable/shallowly frozen.

---

## 9. Object.seal()

Prevents adding or deleting properties, but existing properties can still be changed.

**Mutable:** Yes — existing properties can be modified.

```javascript
const person = {
    name: 'Aniket',
    age: 32
};

Object.seal(person);

person.age = 35;

person.city = 'Mumbai';

delete person.name;

console.log(person);

// {
//     name: 'Aniket',
//     age: 35
// }
```

The `age` property changed, but `city` could not be added and `name` could not be deleted.

---

## 10. Object.create()

Creates a new object using another object as its prototype.

**Immutable:** The prototype object is not modified.

```javascript
const personPrototype = {
    greet() {
        console.log('Hello');
    }
};

const person = Object.create(personPrototype);

person.name = 'Aniket';

console.log(person.name);
// Aniket

person.greet();
// Hello
```

---

## 11. Object.is()

Compares two values and returns `true` or `false`.

**Immutable:** Yes.

```javascript
console.log(Object.is(10, 10));
// true

console.log(Object.is(10, 20));
// false

console.log(Object.is('hello', 'hello'));
// true
```

It is similar to `===`, but has some differences for special values.

```javascript
console.log(Object.is(NaN, NaN));
// true

console.log(Object.is(+0, -0));
// false
```

---

## 12. Object.getOwnPropertyNames()

Returns an array containing the object's own property names.

**Immutable:** Yes.

```javascript
const person = {
    name: 'Aniket',
    age: 32
};

const properties = Object.getOwnPropertyNames(person);

console.log(properties);

// ['name', 'age']
```

---

# Mutable vs Immutable

| Method | Mutable? | Return Value |
|---|---|---|
| `Object.keys()` | No | Array of keys |
| `Object.values()` | No | Array of values |
| `Object.entries()` | No | Array of key-value pairs |
| `Object.fromEntries()` | No | New object |
| `Object.assign()` | **Yes** | Target object |
| `Object.hasOwn()` | No | Boolean |
| `Object.freeze()` | No* | Object |
| `Object.seal()` | No* | Object |
| `Object.create()` | No | New object |
| `Object.is()` | No | Boolean |
| `Object.getOwnPropertyNames()` | No | Array |

> `Object.freeze()` and `Object.seal()` change the object's **property descriptors/state**, so they are better understood as object-state operations rather than normal immutable transformation methods.

---

# Most Important Methods to Remember

```text
Object.keys()
    → Get keys

Object.values()
    → Get values

Object.entries()
    → Get key-value pairs

Object.fromEntries()
    → Convert key-value pairs into an object

Object.assign()
    → Copy/merge properties

Object.hasOwn()
    → Check whether a property exists

Object.freeze()
    → Prevent changes

Object.seal()
    → Prevent adding/removing properties

Object.create()
    → Create an object with a prototype

Object.is()
    → Compare two values
```

# Quick Example

```javascript
const person = {
    name: 'Aniket',
    age: 32,
    city: 'Mumbai'
};

// Get keys
console.log(Object.keys(person));

// Get values
console.log(Object.values(person));

// Get entries
console.log(Object.entries(person));

// Check property
console.log(Object.hasOwn(person, 'name'));

// Convert entries back to object
const newPerson = Object.fromEntries(Object.entries(person));

console.log(newPerson);
```

# Key Points

- `Object.keys()` → returns keys.
- `Object.values()` → returns values.
- `Object.entries()` → returns key-value pairs.
- `Object.fromEntries()` → creates an object from key-value pairs.
- `Object.assign()` → copies properties and can modify the target object.
- `Object.hasOwn()` → checks for an own property.
- `Object.freeze()` → prevents modifications.
- `Object.seal()` → prevents adding/deleting properties.
- `Object.create()` → creates an object with a specified prototype.
- `Object.is()` → compares two values.
- Objects themselves are **mutable by default**.

# Selection of Array Iteration and Utility Methods in JavaScript

JavaScript provides several array iteration and utility methods, including `forEach()`, `map()`, `filter()`, and `reduce()`. Although these methods iterate over array elements, they are designed for different purposes. Selecting the appropriate method depends primarily on the required output and the operation that needs to be performed on the array.

## 1. forEach()

The `forEach()` method is used when an operation needs to be performed on each element of an array, but no new array or accumulated result is required from the iteration. It executes a callback function once for every element and returns `undefined`.

### Example

```javascript
const numbers = [1, 2, 3, 4];

numbers.forEach(number => {
    console.log(number);
});
```

In this example, `forEach()` is appropriate because the purpose is simply to perform an action for each element.

### Common Use Cases

- Printing or logging values
- Updating the DOM
- Calling a function for every element
- Performing side effects
- Executing an operation where the return value is not required

```javascript
const users = [
    { name: 'Aniket' },
    { name: 'Rahul' }
];

users.forEach(user => {
    console.log(`Hello ${user.name}`);
});
```

`forEach()` should generally not be used when the objective is to create a new array or calculate a single accumulated result.

---

## 2. map()

The `map()` method is used when every element of an array needs to be transformed into a new value. It returns a new array containing the transformed elements.

The resulting array normally contains the same number of elements as the original array.

### Example

```javascript
const numbers = [1, 2, 3, 4];

const doubledNumbers = numbers.map(number => {
    return number * 2;
});

console.log(doubledNumbers);
// [2, 4, 6, 8]
```

Here, each element is transformed by multiplying it by `2`.

### Common Use Cases

- Transforming values
- Extracting a particular property from objects
- Converting data from one format to another
- Creating a modified representation of an existing array

```javascript
const users = [
    { name: 'Aniket', age: 32 },
    { name: 'Rahul', age: 25 }
];

const names = users.map(user => user.name);

console.log(names);
// ['Aniket', 'Rahul']
```

### Important Characteristic

`map()` does not modify the original array by itself. It returns a new array.

---

## 3. filter()

The `filter()` method is used when only certain elements of an array need to be selected based on a condition. It returns a new array containing the elements for which the callback function returns `true`.

### Example

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(number => {
    return number % 2 === 0;
});

console.log(evenNumbers);
// [2, 4, 6]
```

In this example, `filter()` selects only the numbers that satisfy the condition.

### Common Use Cases

- Selecting elements based on a condition
- Removing unwanted elements
- Searching for a subset of data
- Filtering objects based on their properties

```javascript
const users = [
    { name: 'Aniket', age: 32 },
    { name: 'Rahul', age: 25 },
    { name: 'Amit', age: 35 }
];

const eligibleUsers = users.filter(user => user.age >= 30);

console.log(eligibleUsers);
```

### Important Characteristic

`filter()` returns a new array, and the resulting array may contain fewer elements than the original array.

---

## 4. reduce()

The `reduce()` method is used when multiple array elements need to be combined into a single result. It maintains an accumulator that is updated during each iteration.

### Example

```javascript
const prices = [100, 200, 300, 400];

const total = prices.reduce((sum, price) => {
    return sum + price;
}, 0);

console.log(total);
// 1000
```

In this example, `reduce()` combines all the prices into a single numerical value.

### Common Use Cases

- Calculating totals
- Calculating averages
- Counting occurrences
- Creating objects from arrays
- Grouping data
- Performing cumulative calculations

```javascript
const numbers = [10, 20, 30, 40];

const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);

console.log(total);
// 100
```

Unlike `map()` and `filter()`, `reduce()` does not necessarily return an array. It can return any value, depending on the accumulator.

---

## 5. Comparison of forEach(), map(), filter(), and reduce()

| Method | Primary Purpose | Return Value | Output Size |
|---|---|---|---|
| `forEach()` | Perform an operation on each element | `undefined` | No new array |
| `map()` | Transform every element | New array | Usually same size |
| `filter()` | Select elements based on a condition | New array | Same or smaller |
| `reduce()` | Combine elements into one result | Single accumulated value | Usually one value |

---

## 6. Choosing the Appropriate Method

The following decision rule can be used when selecting an array method:

```text
Perform an action for every element
        ↓
    forEach()

Transform every element
        ↓
      map()

Select some elements
        ↓
     filter()

Combine elements into one result
        ↓
     reduce()
```

For example, consider the following array:

```javascript
const prices = [100, 200, 300, 400, 500];
```

### Perform an action

```javascript
prices.forEach(price => {
    console.log(price);
});
```

### Transform every element

```javascript
const pricesWithTax = prices.map(price => price * 1.10);
```

### Select specific elements

```javascript
const expensivePrices = prices.filter(price => price > 300);
```

### Calculate a single result

```javascript
const total = prices.reduce((sum, price) => sum + price, 0);
```

---

## 7. Method Chaining

These methods can also be combined when a problem requires multiple operations.

For example, to select prices greater than `200`, increase them by `10%`, and calculate their total:

```javascript
const prices = [100, 200, 300, 400, 500];

const total = prices
    .filter(price => price > 200)
    .map(price => price * 1.10)
    .reduce((sum, price) => sum + price, 0);

console.log(total);
```

In this operation:

1. `filter()` selects the required elements.
2. `map()` transforms the selected elements.
3. `reduce()` combines the transformed elements into a single result.

Method chaining can make data-processing operations concise and expressive when each operation has a clearly defined purpose.

---

## 8. Summary

The choice of an array method should be based on the intended operation:

- **`forEach()`** is used to perform an action on every element without producing a new array.
- **`map()`** is used to transform every element and produce a new array.
- **`filter()`** is used to select elements that satisfy a specified condition.
- **`reduce()`** is used to combine multiple elements into a single accumulated result.

Therefore, `forEach()` is primarily action-oriented, `map()` is transformation-oriented, `filter()` is selection-oriented, and `reduce()` is aggregation-oriented.
