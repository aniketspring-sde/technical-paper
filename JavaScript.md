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
