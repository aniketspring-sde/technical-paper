# Promises



## 1. Why JavaScript needs asynchronous programming

JavaScript runs on a **single thread**. That means it can do **one thing at a time**.

But real applications still need to handle tasks like:

- API calls
- timers
- file reading
- user clicks and keyboard events

JavaScript should not freeze the whole application while waiting for these tasks to finish. That is why we need **asynchronous programming**.

---

## 2. Synchronous JavaScript

**Synchronous code** runs line by line, in order.

```js
console.log("Start");
console.log("Middle");
console.log("End");
```

**Output**

```txt
Start
Middle
End
```

### Short explanation
Each line waits for the previous line to finish.

---

## 3. Asynchronous JavaScript

Some operations take time, such as:

- reading a file
- calling an API
- reading data from a database
- timers like `setTimeout()`

JavaScript starts these tasks and continues running other code.
task queue

```js
console.log("Start");

setTimeout(() => {
  console.log("Task completed");
}, 2000);

console.log("End");
```

**Output**

```txt
Start
End
Task completed
```

### Short explanation
`setTimeout()` is asynchronous, so JavaScript does not wait 2 seconds before running the next line.

---

## 4. Callbacks

Before Promises became common, JavaScript mostly used **callbacks** for asynchronous work.

A **callback** is a function passed into another function so it can be executed later.

```js
function getData(callback) {
  setTimeout(() => {
    callback("Data received");
  }, 2000);
}

getData((data) => {
  console.log(data);
});
```

**Output**

```txt
Data received
```

### Short explanation
The callback runs only after the asynchronous task is finished.

---

## 5. Problem with callbacks: Callback Hell

One callback is easy to manage. But when many async tasks depend on each other, callbacks become deeply nested.

```js
getUser(1, (user) => {
  getOrders(user.id, (orders) => {
    getOrderDetails(orders[0].id, (order) => {
      processPayment(order, (payment) => {
        sendConfirmation(payment, (message) => {
          console.log(message);
        });
      });
    });
  });
});
```

### Why this is bad

- hard to read
- hard to debug
- hard to maintain
- error handling becomes messy

This deeply nested structure is called **callback hell**.

---

## 6. Inversion of Control

With callbacks, you give your function to another function or library and trust it to call your function correctly.

This is called **Inversion of Control**.

### Simple meaning
You lose control over:

- **when** your callback runs
- **how many times** it runs
- **whether** it runs at all

This was another reason Promises became important.

---

## 7. Call Stack, Task Queue, Microtask Queue, and Event Loop

To understand Promises better, you should know these terms.

### Call Stack
The Call Stack is where JavaScript runs synchronous code.

### Task Queue
Callbacks from APIs like `setTimeout()` go into the **Task Queue**.

### Microtask Queue
Promise callbacks like `.then()` and `.catch()` go into the **Microtask Queue**.

### Event Loop
The **Event Loop** keeps checking whether the Call Stack is empty.
When it is empty, it moves ready callbacks into the Call Stack.

### Important rule
JavaScript runs:

1. synchronous code first
2. microtasks next
3. task queue callbacks after that

---

## 8. Microtask example

```js
console.log("Start");

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Output**

```txt
Start
End
Promise
```

### Short explanation
The `.then()` callback goes to the **Microtask Queue**, so it runs after synchronous code finishes.

---

## 9. Microtask vs Task Queue example

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Output**

```txt
Start
End
Promise
Timeout
```

### Short explanation
Even though `setTimeout(..., 0)` has zero delay, Promise callbacks run first because **Microtask Queue** has higher priority than **Task Queue**.

---

## 10. Why Promises were introduced

Promises were introduced to make asynchronous code easier to:

- read
- organize
- chain
- control
- handle errors

### Simple definition
A **Promise** is an object that represents the eventual success or failure of an asynchronous operation.

### Easy real-life example
Think of a restaurant order:

- **pending** -> food is being prepared
- **fulfilled** -> food is ready
- **rejected** -> order failed or was cancelled

---

## 11. Promise states

Every Promise has one of these three states:

### 1. Pending
The operation is still running.

### 2. Fulfilled
The operation completed successfully.

### 3. Rejected
The operation failed.

A Promise can settle only **once**.
After it becomes fulfilled or rejected, it cannot change again.

### Example

```js
const promise = new Promise((resolve, reject) => {
  resolve("First result");
  reject("Error");
  resolve("Second result");
});

promise.then((result) => {
  console.log(result);
});
```

**Output**

```txt
First result
```

### Short explanation
Only the first successful settle counts.

---

## 12. Creating a Promise

```js
const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Operation successful");
  } else {
    reject(new Error("Operation failed"));
  }
});
```

### Short explanation

- `resolve()` marks the Promise as fulfilled
- `reject()` marks the Promise as rejected

---

## 13. Consuming a Promise

The main instance methods are:

- `.then()`
- `.catch()`
- `.finally()`

---

## 14. `.then()`

`.then()` handles a fulfilled Promise.

```js
const promise = new Promise((resolve) => {
  resolve("User data received");
});

promise.then((result) => {
  console.log(result);
});
```

**Output**

```txt
User data received
```

### Short explanation
The value passed to `resolve()` becomes the value inside `.then()`.

---

## 15. `.catch()`

`.catch()` handles Promise rejection.

```js
const promise = new Promise((resolve, reject) => {
  reject(new Error("Server is unavailable"));
});

promise.catch((error) => {
  console.log(error.message);
});
```

**Output**

```txt
Server is unavailable
```

### Short explanation
The value passed to `reject()` becomes the error inside `.catch()`.

---

## 16. `.finally()`

`.finally()` runs whether the Promise succeeds or fails.

```js
const promise = new Promise((resolve) => {
  resolve("Data loaded");
});

promise
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error.message);
  })
  .finally(() => {
    console.log("Operation finished");
  });
```

**Output**

```txt
Data loaded
Operation finished
```

### Short explanation
Use `.finally()` for cleanup work such as hiding a loader.

---

## 17. Complete Promise example

```js
function checkAge(age) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (age >= 18) {
        resolve("You are eligible");
      } else {
        reject(new Error("You are not eligible"));
      }
    }, 1000);
  });
}

checkAge(22)
  .then((message) => {
    console.log(message);
  })
  .catch((error) => {
    console.log(error.message);
  })
  .finally(() => {
    console.log("Age verification completed");
  });
```

**Output**

```txt
You are eligible
Age verification completed
```

---

## 18. Returning a Promise from a function

Most Promise-based functions return a Promise.

```js
function getUser() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({
        id: 1,
        name: "Abhi"
      });
    }, 1000);
  });
}

const result = getUser();
console.log(result);
```

**Output**

```txt
Promise { <pending> }
```

To access the actual value:

```js
getUser().then((user) => {
  console.log(user);
});
```

**Output**

```txt
{ id: 1, name: 'Abhi' }
```

---

## 19. Promise chaining

One of the biggest advantages of Promises is **chaining**.

Both `.then()` and `.catch()` return a **new Promise**, so we can connect steps in sequence.

```js
Promise.resolve(5)
  .then((number) => {
    return number * 2;
  })
  .then((number) => {
    return number + 10;
  })
  .then((result) => {
    console.log(result);
  });
```

**Output**

```txt
20
```

### Short explanation
If you return a normal value from `.then()`, JavaScript automatically wraps it in a Promise.

Internally it behaves like this:

```js
return Promise.resolve(value);
```

---

## 20. What if you do not return anything?

```js
Promise.resolve(5)
  .then((number) => {
    console.log(number);
  })
  .then((value) => {
    console.log(value);
  });
```

**Output**

```txt
5
undefined
```

### Short explanation
If a `.then()` callback returns nothing, it returns `undefined`.

---

## 21. Returning another Promise

You can return a Promise from inside `.then()`.
The next `.then()` waits for it to finish.

```js
Promise.resolve(5)
  .then((number) => {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve(number * 2);
      }, 2000);
    });
  })
  .then((result) => {
    console.log(result);
  });
```

**Output after 2 seconds**

```txt
10
```

---

## 22. Error handling in a Promise chain

If any Promise in the chain fails, control goes to `.catch()`.

```js
Promise.resolve(5)
  .then(() => {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        reject(new Error("how"));
      }, 2000);
    });
  })
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error.message);
  });
```

**Output**

```txt
how
```

---

## 23. Errors can also be thrown rejected Promise.

You do not always need to call `reject()`.
If an error is thrown inside a Promise or `.then()`, JavaScript converts it into a rejected Promise.

```js
Promise.resolve(5)
  .then(() => {
    throw new Error("Boom!");
  })
  .catch((err) => {
    console.log(err.message);
  });
```

**Output**

```txt
Boom!
```

---

## 24. Recovering from an error

A `.catch()` can return a fallback value, and the chain can continue.

```js
Promise.reject(new Error("Server failed"))
  .catch((error) => {
    console.log(error.message);
    return "Default data";
  })
  .then((data) => {
    console.log(data);
  });
```

**Output**

```txt
Server failed
Default data
```

---

## 25. Network request example

One of the biggest uses of Promises is making API requests.

```js
fetch("https://jsonplaceholder.typicode.com/users")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

### Short explanation
JavaScript does not stop the whole program while waiting for the server. When the response comes back, the Promise is fulfilled.

---

# Promise Methods

## 26. `Promise.resolve()`

Creates a Promise that is already fulfilled.

```js
Promise.resolve("Hello")
  .then((value) => console.log(value));
```

**Output**

```txt
Hello
```

### Why we use it
When a function is expected to return a Promise, but we already have the value.

---

## 27. `Promise.reject()`

Creates a Promise that is already rejected.

```js
Promise.reject(new Error("Invalid"))
  .catch((error) => console.log(error.message));
```

**Output**

```txt
Invalid
```

### Why we use it
When we want to immediately return a failed Promise.

---

## 28. `Promise.all()`

Runs multiple Promises at the same time and waits until **all of them succeed**.
If one fails, the whole result fails.

```js
const p1 = Promise.resolve("User");
const p2 = Promise.resolve("Orders");
const p3 = Promise.resolve("Products");

Promise.all([p1, p2, p3])
  .then((results) => {
    console.log(results);
  });
```

**Output**

```txt
[ 'User', 'Orders', 'Products' ]
```

### Best use case
Use when all tasks are independent, but you need every one of them to succeed.

---

## 29. `Promise.allSettled()`

Waits until every Promise finishes, whether it succeeds or fails.

```js
const p1 = Promise.resolve("User");
const p2 = Promise.reject("Network Error");
const p3 = Promise.resolve("Products");

Promise.allSettled([p1, p2, p3])
  .then((results) => {
    console.log(results);
  });
```

**Output**

```txt
[
  { status: 'fulfilled', value: 'User' },
  { status: 'rejected', reason: 'Network Error' },
  { status: 'fulfilled', value: 'Products' }
]
```

### Best use case
Use when you want the result of every task, even failed ones.

---

## 30. `Promise.any()`

Returns the **first fulfilled Promise**.
Rejected Promises are ignored unless all Promises fail.

```js
const p1 = Promise.reject("Server A");
const p2 = Promise.resolve("Server B");
const p3 = Promise.resolve("Server C");

Promise.any([p1, p2, p3])
  .then((result) => {
    console.log(result);
  });
```

**Output**

```txt
Server B
```

### Best use case
Use when you need the first successful result from multiple sources.

---

## 31. `Promise.race()`

Returns the **first settled Promise**.
Settled means fulfilled or rejected.

```js
const p1 = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Task 1");
  }, 3000);
});

const p2 = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Task 2");
  }, 1000);
});

Promise.race([p1, p2])
  .then((result) => {
    console.log(result);
  });
```

**Output**

```txt
Task 2
```

### Best use case
Use when you want whichever finishes first, such as request timeout logic.

---

## 32. Quick comparison table

| Method | Success condition | Failure condition | Returns |
|---|---|---|---|
| `Promise.resolve()` | immediately fulfilled | never | fulfilled Promise |
| `Promise.reject()` | never | immediately rejected | rejected Promise |
| `Promise.all()` | all Promises fulfill | any Promise rejects | array of values |
| `Promise.allSettled()` | waits for all | does not fail because of individual rejection | array of result objects |
| `Promise.any()` | first Promise fulfills | all Promises reject | first fulfilled value |
| `Promise.race()` | first Promise settles | first Promise may reject | first settled value or error |

---

## 33. Which method should you use?

| Situation | Best choice |
|---|---|
| Return an already successful Promise | `Promise.resolve()` |
| Return an already failed Promise | `Promise.reject()` |
| Run many tasks and require all to succeed | `Promise.all()` |
| Run many tasks and inspect every result | `Promise.allSettled()` |
| Need the first successful result | `Promise.any()` |
| Need whichever finishes first | `Promise.race()` |

---

## 34. Final summary


- synchronous JavaScript
- asynchronous JavaScript
- callbacks
- callback hell
- event loop
- task queue
- microtask queue

Promises solve the main problems of callbacks by making asynchronous code:

- cleaner
- easier to read
- easier to chain
- easier to handle errors
