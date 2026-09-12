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
## truthy and falsy values.
