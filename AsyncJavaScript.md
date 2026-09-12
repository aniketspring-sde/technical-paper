


## 1. How Does JavaScript Execute Code?

JavaScript is a **single-threaded, synchronous programming language** at its core. This means JavaScript code is executed one statement at a time on a single main thread.

A JavaScript runtime, such as a browser or Node.js, provides the environment required to execute JavaScript.

The basic execution flow is:

```text
JavaScript Code
      ↓
Parsing
      ↓
Execution Context
      ↓
Call Stack
      ↓
JavaScript Engine
      ↓
Host APIs / Event Loop for asynchronous operations
```

### JavaScript Engine

A JavaScript engine executes JavaScript code.

Examples:

- Chrome → V8
- Firefox → SpiderMonkey
- Safari → JavaScriptCore

When JavaScript code is executed:

1. The code is parsed.
2. An execution context is created.
3. Variables and functions are prepared.
4. Statements are executed.
5. Function calls are placed on the call stack.
6. Functions are removed from the stack after execution.

Example:

```javascript
console.log("Start");

function greet() {
    console.log("Hello");
}

greet();

console.log("End");
```

Output:

```text
Start
Hello
End
```

The function `greet()` is pushed onto the call stack, executed, and then removed from the stack.

### Call Stack

The **call stack** keeps track of currently executing functions.

```javascript
function first() {
    second();
}

function second() {
    console.log("Hello");
}

first();
```

The stack changes approximately as follows:

```text
first()
second()
console.log()
```

After `console.log()` finishes:

```text
first()
second()
```

After `second()` finishes:

```text
first()
```

Finally:

```text
empty
```

The call stack follows **LIFO (Last In, First Out)**.

---

# 2. Synchronous vs Asynchronous Code

## Synchronous Code

Synchronous code executes **one operation at a time and waits for the current operation to finish before moving to the next operation**.

```javascript
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

The second statement cannot execute until the first statement finishes.

---

## Asynchronous Code

Asynchronous code allows an operation to be started without blocking the execution of other JavaScript code.

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 2000);

console.log("C");
```

Output:

```text
A
C
B
```

`setTimeout()` starts a timer, but JavaScript does not wait for the timer to finish. It continues executing the next statement.

### Difference

| Synchronous | Asynchronous |
|---|---|
| Executes sequentially | Allows work to complete later |
| Blocks subsequent execution when an operation is running | Does not necessarily block JavaScript execution |
| Easier to understand | Requires callbacks, promises, or async/await |
| Example: normal function call | Example: `setTimeout()`, `fetch()` |

An important point is that **asynchronous behavior is not achieved because JavaScript has multiple JavaScript threads**. The JavaScript execution itself normally occurs on one thread, while the runtime environment can perform or wait for operations outside the JavaScript call stack.

---

# 3. Ways to Make Code Asynchronous

Common approaches are:

1. Callbacks
2. Promises
3. `async/await`
4. Browser APIs such as timers, network APIs and events

### Callback

```javascript
setTimeout(() => {
    console.log("Task completed");
}, 1000);
```

### Promise

```javascript
fetch("/users")
    .then(response => response.json())
    .then(users => console.log(users));
```

### Async/Await

```javascript
async function getUsers() {
    const response = await fetch("/users");
    const users = await response.json();

    console.log(users);
}
```

`async/await` is built on top of promises. It provides a more synchronous-looking syntax for writing asynchronous code.

---

# 4. What Are Web Browser APIs?

JavaScript itself does not provide every feature required by a web browser.

The browser provides additional APIs called **Web APIs** or **Browser APIs**.

Examples include:

- `setTimeout()`
- `setInterval()`
- `fetch()`
- DOM APIs
- Event APIs
- Geolocation API
- Web Storage API
- WebSocket API

Example:

```javascript
setTimeout(() => {
    console.log("Timer completed");
}, 2000);
```

`setTimeout()` is provided by the browser environment rather than being a core JavaScript language feature.

Similarly:

```javascript
fetch("https://example.com/users");
```

uses a web platform API to perform network communication.

Node.js provides its own runtime APIs, such as:

```javascript
fs.readFile()
```

Therefore, it is useful to distinguish:

```text
JavaScript
   ↓
JavaScript Engine

Browser
   ↓
JavaScript Engine + Web APIs

Node.js
   ↓
JavaScript Engine + Node.js APIs
```

---

# 5. What Is the Event Loop?

The **event loop** is the mechanism that coordinates asynchronous operations with the JavaScript call stack.

A simplified browser model is:

```text
             JavaScript
                 |
                 v
            Call Stack
                 |
                 v
              Web APIs
                 |
                 v
       Callback / Task Queues
                 |
                 v
             Event Loop
                 |
                 +------> Call Stack
```

Suppose we execute:

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("End");
```

Output:

```text
Start
End
Timer
```

Even though the timer is `0` milliseconds, its callback does not execute immediately.

The browser schedules the callback, and the event loop can move it to the appropriate task queue only after the current JavaScript execution has completed.

The event loop continuously checks whether the call stack is available for queued work.

---

# 6. Microtasks and Macrotasks

JavaScript runtimes have different categories of queued work.

Promise handlers such as:

```javascript
.then()
.catch()
.finally()
```

are scheduled as **microtasks**.

Timer callbacks such as:

```javascript
setTimeout()
setInterval()
```

are generally scheduled as **tasks** (often informally called macrotasks).

Example:

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

Promise.resolve().then(() => {
    console.log("C");
});

console.log("D");
```

Output:

```text
A
D
C
B
```

The synchronous code executes first. Then pending microtasks are processed before the next task is taken.

---

# 7. What Is Callback Hell?

A **callback** is a function passed to another function to be executed later.

Example:

```javascript
getUser(function(user) {
    console.log(user);
});
```

When several asynchronous operations depend on one another, callbacks can become deeply nested.

```javascript
getUser(function(user) {

    getOrders(user.id, function(orders) {

        getPayment(orders[0].id, function(payment) {

            sendNotification(payment, function(result) {

                console.log(result);

            });

        });

    });

});
```

This is called **callback hell**.

Problems with callback hell include:

- Deep nesting
- Difficult readability
- Difficult error handling
- Difficult maintenance
- Difficult debugging
- Complex control flow

Promises were introduced to provide a cleaner way to represent and compose asynchronous operations.

---

# 8. What Is Inversion of Control in Callbacks?

**Inversion of Control (IoC)** occurs when we give control of part of our program to another function or API.

Consider:

```javascript
getUser(function(user) {
    console.log(user);
});
```

We provide our callback to `getUser()` and trust `getUser()` to:

- Call it
- Call it at the correct time
- Call it with the correct arguments
- Potentially handle errors correctly
- Ideally call it only once

Therefore, we have transferred control over when and how the callback executes to another piece of code.

This is one of the disadvantages of callback-based programming.

Promises reduce this problem because the promise represents the eventual result and provides a standardized way to consume it.

---

# 9. What Is a Promise?

A **Promise** is an object that represents the eventual completion or failure of an asynchronous operation.

A promise can represent a value that is:

- Not available yet
- Available successfully
- Failed

Example:

```javascript
const promise = fetch("/users");
```

The `fetch()` function immediately returns a Promise.

The actual response may become available later.

Conceptually:

```text
Promise
   |
   +-- Pending
   |
   +-- Fulfilled
   |
   +-- Rejected
```

---

# 10. How to Create a New Promise

A new Promise can be created using the `Promise` constructor.

Syntax:

```javascript
const promise = new Promise((resolve, reject) => {
    // asynchronous operation
});
```

Example:

```javascript
const promise = new Promise((resolve, reject) => {

    const success = true;

    if (success) {
        resolve("Operation successful");
    } else {
        reject("Operation failed");
    }

});
```

A better practice is to reject with an `Error` object:

```javascript
const promise = new Promise((resolve, reject) => {

    if (success) {
        resolve("Success");
    } else {
        reject(new Error("Operation failed"));
    }

});
```

`resolve()` fulfills the promise.

`reject()` rejects the promise.

---

# 11. States of a Promise

A Promise has three important states.

## Pending

The asynchronous operation has not completed.

```text
Pending
```

## Fulfilled

The asynchronous operation completed successfully.

```text
Fulfilled
```

## Rejected

The asynchronous operation failed.

```text
Rejected
```

The state transition is:

```text
             resolve()
Pending -----------------> Fulfilled

Pending
   |
   | reject()
   v
Rejected
```

A settled promise cannot change its state again.

For example:

```javascript
const promise = new Promise((resolve, reject) => {
    resolve("Success");
    reject("Failure");
});
```

The promise remains fulfilled because the first settlement wins.

---

# 12. How to Consume an Existing Promise

Promises are commonly consumed using:

```javascript
.then()
.catch()
.finally()
```

Example:

```javascript
fetch("/users")
    .then(response => response.json())
    .then(users => {
        console.log(users);
    })
    .catch(error => {
        console.error(error);
    })
    .finally(() => {
        console.log("Request completed");
    });
```

---

# 13. Promise Chaining Using `.then()`

`.then()` allows asynchronous operations to be connected together.

```javascript
getUser()
    .then(user => {
        return getOrders(user.id);
    })
    .then(orders => {
        return getPayment(orders[0].id);
    })
    .then(payment => {
        console.log(payment);
    });
```

The important rule is:

> A `.then()` returns a new Promise.

Therefore, its returned value can be passed to the next `.then()`.

Example:

```javascript
Promise.resolve(10)
    .then(value => {
        return value * 2;
    })
    .then(value => {
        return value + 5;
    })
    .then(value => {
        console.log(value);
    });
```

Output:

```text
25
```

The chain is:

```text
10
 ↓
20
 ↓
25
```

---

# 14. Handling Errors Using `.catch()`

`.catch()` handles a rejected promise.

```javascript
Promise.reject(new Error("Something went wrong"))
    .catch(error => {
        console.error(error.message);
    });
```

Output:

```text
Something went wrong
```

A common pattern is:

```javascript
doSomething()
    .then(result => {
        return doSomethingElse(result);
    })
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.error(error);
    });
```

---

# 15. `finally()` in a Promise Chain

`finally()` executes after a promise settles, regardless of whether it was fulfilled or rejected.

```javascript
fetch("/users")
    .then(response => response.json())
    .catch(error => {
        console.error(error);
    })
    .finally(() => {
        console.log("Request completed");
    });
```

It is useful for cleanup operations such as:

- Hiding a loading indicator
- Closing a resource
- Resetting UI state
- Releasing temporary resources

Example:

```javascript
showLoading();

fetch("/users")
    .then(response => response.json())
    .then(users => {
        console.log(users);
    })
    .catch(error => {
        console.error(error);
    })
    .finally(() => {
        hideLoading();
    });
```

---

# 16. What Happens When an Error Is Thrown Inside `.then()` and There Is a `.catch()`?

An error thrown inside a `.then()` callback causes the promise returned by that `.then()` to become rejected.

```javascript
Promise.resolve("Hello")
    .then(value => {
        throw new Error("Something went wrong");
    })
    .catch(error => {
        console.error(error.message);
    });
```

Output:

```text
Something went wrong
```

The error travels down the promise chain until a rejection handler such as `.catch()` handles it.

Conceptually:

```text
Promise
   ↓
.then()
   ↓
Error thrown
   ↓
Rejected Promise
   ↓
.catch()
```

---

# 17. What Happens When an Error Is Thrown and There Is No `.catch()`?

If a promise is rejected and no rejection handler handles it, the rejection becomes **unhandled**.

Example:

```javascript
Promise.resolve()
    .then(() => {
        throw new Error("Failure");
    });
```

There is no `.catch()`.

The runtime reports an unhandled promise rejection.

Therefore, asynchronous code should have an appropriate error-handling strategy.

---

# 18. Why Is `.catch()` Commonly Placed Toward the End?

Consider:

```javascript
doStep1()
    .then(doStep2)
    .then(doStep3)
    .catch(handleError);
```

This allows one error handler to handle failures from any previous step in the chain.

For example:

```text
doStep1()
   ↓
doStep2()
   ↓
doStep3()
   ↓
catch()
```

If `.catch()` is placed earlier:

```javascript
doStep1()
    .catch(handleError)
    .then(doStep2)
    .then(doStep3);
```

the `catch()` may handle an earlier failure and return a fulfilled value. The chain can then continue.

Therefore, placing a final `.catch()` toward the end is a common pattern when the intention is to handle errors from the entire preceding chain.

However, `.catch()` does **not** have to be at the end. It can be intentionally placed earlier when a specific error should be recovered from locally.

---

# 19. Consuming Multiple Promises by Chaining

Promises can be chained when one operation depends on the result of the previous operation.

```javascript
getUser()
    .then(user => {
        return getOrders(user.id);
    })
    .then(orders => {
        return getPayment(orders[0].id);
    })
    .then(payment => {
        console.log(payment);
    })
    .catch(error => {
        console.error(error);
    });
```

This is appropriate when the operations have a dependency:

```text
User
 ↓
Orders
 ↓
Payment
```

The next operation cannot begin until the previous result is available.

---

# 20. Consuming Multiple Promises Using `Promise.all()`

`Promise.all()` is useful when multiple independent promises need to be executed and all results are required.

```javascript
const userPromise = fetch("/user");
const ordersPromise = fetch("/orders");
const productsPromise = fetch("/products");

Promise.all([
    userPromise,
    ordersPromise,
    productsPromise
])
.then(results => {
    console.log(results);
})
.catch(error => {
    console.error(error);
});
```

The promises can progress concurrently.

The result is an array corresponding to the input order.

```javascript
Promise.all([
    Promise.resolve("A"),
    Promise.resolve("B"),
    Promise.resolve("C")
])
.then(results => {
    console.log(results);
});
```

Output:

```text
["A", "B", "C"]
```

### Important behavior

`Promise.all()` rejects when **any input promise rejects**.

```javascript
Promise.all([
    Promise.resolve("A"),
    Promise.reject(new Error("Failure")),
    Promise.resolve("C")
])
.catch(error => {
    console.error(error.message);
});
```

Output:

```text
Failure
```

Use `Promise.all()` when:

> All operations are required for the overall operation to succeed.

---

# 21. Promise Chaining vs `Promise.all()`

### Sequential dependency

Use chaining:

```javascript
getUser()
    .then(user => getOrders(user.id))
    .then(orders => getPayment(orders[0].id));
```

Here, each operation depends on the previous result.

### Independent operations

Use `Promise.all()`:

```javascript
Promise.all([
    getUsers(),
    getProducts(),
    getOrders()
])
.then(([users, products, orders]) => {
    console.log(users);
    console.log(products);
    console.log(orders);
});
```

Here, the operations are independent.

---

# 22. Error Handling with Promises

A standard pattern is:

```javascript
doSomething()
    .then(result => {
        return processResult(result);
    })
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.error(error);
    })
    .finally(() => {
        console.log("Finished");
    });
```

Errors can originate from:

- A rejected promise
- An exception thrown inside `.then()`
- A function returning a rejected promise

Example:

```javascript
Promise.resolve()
    .then(() => {
        throw new Error("Database error");
    })
    .catch(error => {
        console.error(error.message);
    });
```

The thrown error becomes a rejected promise and can be handled by `.catch()`.

---

# 23. Why Is Error Handling Important When Using Promises?

Promise-based operations are asynchronous. Therefore, an error may occur later, after the original function has already returned.

Without proper error handling:

- Failures may go unnoticed.
- The application may enter an invalid state.
- Users may receive incorrect results.
- Debugging becomes difficult.
- Unhandled promise rejections may occur.

For this reason, asynchronous code should have an appropriate strategy for handling rejected promises.

Example:

```javascript
fetch("/users")
    .then(response => response.json())
    .catch(error => {
        console.error("Failed to load users:", error);
    });
```

Error handling should also provide meaningful recovery or reporting rather than simply hiding the error.

---

# 24. Promisifying a Callback-Based Function

**Promisification** means converting a callback-based asynchronous function into a function that returns a Promise.

Suppose we have:

```javascript
function delay(callback) {
    setTimeout(() => {
        callback("Completed");
    }, 1000);
}
```

We can create a Promise-based version:

```javascript
function delayPromise(milliseconds) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve("Completed");
        }, milliseconds);
    });
}
```

Consume it:

```javascript
delayPromise(1000)
    .then(result => {
        console.log(result);
    });
```

Output after one second:

```text
Completed
```

---

# 25. Promisifying `fs.readFile()`

Node.js provides callback-based APIs such as:

```javascript
const fs = require("fs");

fs.readFile("data.txt", "utf8", (error, data) => {
    if (error) {
        console.error(error);
        return;
    }

    console.log(data);
});
```

A Promise-based version can be created manually:

```javascript
const fs = require("fs");

function readFilePromise(fileName) {
    return new Promise((resolve, reject) => {
        fs.readFile(fileName, "utf8", (error, data) => {

            if (error) {
                reject(error);
                return;
            }

            resolve(data);
        });
    });
}
```

Now it can be consumed using promises:

```javascript
readFilePromise("data.txt")
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error(error);
    });
```

Node.js also provides a built-in Promise-based API:

```javascript
const fs = require("fs").promises;

fs.readFile("data.txt", "utf8")
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error(error);
    });
```

Modern Node.js code can also use:

```javascript
const { readFile } = require("fs/promises");

readFile("data.txt", "utf8")
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error(error);
    });
```

---

# 26. `Promise.resolve()`

`Promise.resolve()` creates a fulfilled Promise from a value.

```javascript
Promise.resolve("Hello")
    .then(value => {
        console.log(value);
    });
```

Output:

```text
Hello
```

It can also be used to convert an existing value into a Promise.

```javascript
const promise = Promise.resolve(100);

console.log(promise);
```

If the value passed to `Promise.resolve()` is already a Promise, it generally returns that Promise rather than creating an unnecessary new one.

---

# 27. `Promise.reject()`

`Promise.reject()` creates an immediately rejected Promise.

```javascript
Promise.reject(new Error("Something went wrong"))
    .catch(error => {
        console.error(error.message);
    });
```

Output:

```text
Something went wrong
```

It is useful for creating a rejected Promise programmatically.

---

# 28. `Promise.all()`

`Promise.all()` waits for all input promises to fulfill.

```javascript
const p1 = Promise.resolve("A");
const p2 = Promise.resolve("B");
const p3 = Promise.resolve("C");

Promise.all([p1, p2, p3])
    .then(results => {
        console.log(results);
    });
```

Output:

```text
["A", "B", "C"]
```

If one rejects:

```javascript
Promise.all([
    Promise.resolve("A"),
    Promise.reject(new Error("Failed")),
    Promise.resolve("C")
])
.catch(error => {
    console.error(error.message);
});
```

The returned Promise rejects.

Use `Promise.all()` when all operations are required.

---

# 29. `Promise.allSettled()`

`Promise.allSettled()` waits for **all promises to settle**, regardless of whether they fulfill or reject.

```javascript
Promise.allSettled([
    Promise.resolve("A"),
    Promise.reject(new Error("Failed")),
    Promise.resolve("C")
])
.then(results => {
    console.log(results);
});
```

The result contains the status of every promise.

Conceptually:

```javascript
[
    { status: "fulfilled", value: "A" },
    { status: "rejected", reason: Error },
    { status: "fulfilled", value: "C" }
]
```

Unlike `Promise.all()`, one rejection does not cause the returned Promise to reject.

Use `Promise.allSettled()` when:

> You need the result of every operation, including failures.

---

# 30. `Promise.any()`

`Promise.any()` fulfills as soon as **the first input Promise fulfills**.

```javascript
Promise.any([
    Promise.reject(new Error("Server 1 failed")),
    Promise.resolve("Server 2 response"),
    Promise.resolve("Server 3 response")
])
.then(result => {
    console.log(result);
})
.catch(error => {
    console.error(error);
});
```

Output:

```text
Server 2 response
```

Rejected promises are ignored until a promise fulfills.

If **all** promises reject, `Promise.any()` rejects with an `AggregateError`.

Use `Promise.any()` when:

> You need the first successful result.

---

# 31. `Promise.race()`

`Promise.race()` settles as soon as the **first input Promise settles**.

Settled means either:

- Fulfilled
- Rejected

Example:

```javascript
const fast = new Promise(resolve => {
    setTimeout(() => resolve("Fast"), 1000);
});

const slow = new Promise(resolve => {
    setTimeout(() => resolve("Slow"), 3000);
});

Promise.race([fast, slow])
    .then(result => {
        console.log(result);
    });
```

Output:

```text
Fast
```

If the first promise rejects:

```javascript
Promise.race([
    Promise.reject(new Error("Failed")),
    Promise.resolve("Success")
])
.catch(error => {
    console.error(error.message);
});
```

The result is rejected because the first settled promise was rejected.

---

# 32. Comparison of Promise Combinators

| Method | Resolves when | Rejects when | Main Use |
|---|---|---|---|
| `Promise.resolve()` | Immediately | — | Create a fulfilled Promise |
| `Promise.reject()` | — | Immediately | Create a rejected Promise |
| `Promise.all()` | All fulfill | Any one rejects | Need all successful results |
| `Promise.allSettled()` | All settle | Never because of input rejection | Need every result |
| `Promise.any()` | First fulfills | All reject | Need first successful result |
| `Promise.race()` | First settles | First settled promise rejects | Need first completed result |

---

# 33. `Promise.all()` vs `Promise.allSettled()`

### `Promise.all()`

```javascript
Promise.all([
    task1(),
    task2(),
    task3()
])
.then(results => {
    console.log(results);
})
.catch(error => {
    console.error(error);
});
```

One failure causes the returned Promise to reject.

### `Promise.allSettled()`

```javascript
Promise.allSettled([
    task1(),
    task2(),
    task3()
])
.then(results => {
    console.log(results);
});
```

All operations are allowed to finish.

This is useful when individual failures should not prevent the application from seeing the results of other operations.

---

# 34. `Promise.any()` vs `Promise.race()`

These methods are often confused.

### `Promise.any()`

Waits for the **first fulfilled** promise.

```text
Reject
Reject
Fulfilled  ← Result
Fulfilled
```

### `Promise.race()`

Waits for the **first settled** promise.

```text
Reject  ← Result
Fulfilled
Fulfilled
```

Therefore:

```text
Promise.any()
→ First SUCCESS

Promise.race()
→ First COMPLETION
```

---

# 35. Overall Asynchronous JavaScript Model

The concepts discussed above can be connected together as follows:

```text
                  JavaScript Code
                        |
                        v
                  Call Stack
                        |
                        v
                Runtime / Host APIs
                        |
             +----------+----------+
             |                     |
          Timers               Network
             |                     |
             +----------+----------+
                        |
                        v
                  Queues / Jobs
                        |
                        v
                    Event Loop
                        |
                        v
                   Call Stack
```

Promises provide a structured way of representing asynchronous results:

```text
Asynchronous Operation
        |
        v
     Promise
        |
   +----+----+
   |         |
Success    Failure
   |         |
 then()    catch()
   |
finally()
```

---

# 36. Summary

JavaScript executes synchronous code using a call stack. Although JavaScript execution is single-threaded, the surrounding runtime environment provides APIs for asynchronous operations.

The event loop coordinates completed asynchronous work with the JavaScript call stack.

Callback-based programming can lead to callback hell and inversion of control. Promises provide a structured abstraction for asynchronous operations.

The major Promise concepts are:

- A Promise represents an eventual result.
- A Promise can be `pending`, `fulfilled`, or `rejected`.
- `.then()` handles successful results and enables chaining.
- `.catch()` handles rejected promises and errors.
- `.finally()` executes after settlement regardless of success or failure.
- Errors thrown inside `.then()` become rejected promises.
- `Promise.all()` waits for all promises and fails if one rejects.
- `Promise.allSettled()` waits for every promise regardless of success or failure.
- `Promise.any()` waits for the first successful promise.
- `Promise.race()` waits for the first settled promise.
- Callback-based APIs can be converted into Promise-based APIs through promisification.
- `async/await` provides a cleaner syntax for consuming promises.

Understanding the relationship between the **call stack, runtime APIs, queues, event loop, callbacks, and promises** is essential before moving to more advanced asynchronous JavaScript programming.
