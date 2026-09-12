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
