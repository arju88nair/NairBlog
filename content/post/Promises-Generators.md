---
title: "Promises and Generators"
date: 2018-11-30T21:49:43+05:30
draft: false
tags : [
"Javascript",
"Interview",
"ES6"
]
---

# Promises
> A proxy for a value not necessarily known when the promise is created.

> An asynchronous function is a function which operates asynchronously via the event loop, using an implicit Promise to return its result.

> then() consumes a Promise while await waits for a promise to be resolved


Once a promise has been called, it will start in pending state. This means that the caller function continues the execution, while it waits for the promise to do its own processing, and give the caller function some feedback.

The function waits for it to either return the promise in a resolved state, or in a rejected state

```
let done = true

const isItDoneYet = new Promise(
  (resolve, reject) => {
    if (done) {
      const workDone = 'Here is the thing I built'
      resolve(workDone)
    } else {
      const why = 'Still working on something else'
      reject(why)
    }
  }
)


// To consume

const checkIfItsDone = () => {
  isItDoneYet
    .then((ok) => {
      console.log(ok)
    })
    .catch((err) => {
      console.error(err)
    })
}

```

## Chaining promises

```
const status = (response) => {
  if (response.status >= 200 && response.status < 300) {
    return Promise.resolve(response)
  }
  return Promise.reject(new Error(response.statusText))
}

const json = (response) => response.json()

fetch('/todos.json')
  .then(status)
  .then(json)
  .then((data) => { console.log('Request succeeded with JSON response', data) })
  .catch((error) => { console.log('Request failed', error) })
  ```
  - `Fetch()` is called.
  - If resolved, calls `status()` (checking HTTPcode and all), else the `catch`.
  - Then `data()`


  ---- 
# Async Await

An `async` function can contain an `await` expression that pauses the execution of the `async` function and waits for the passed Promise's resolution, and then resumes the `async` function's execution and returns the resolved value. The `await` keyword is only valid inside `async` functions.


```
function scaryClown() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('🤡');
    }, 2000);
  });
}

async function msg() {
  const msg = await scaryClown();
  console.log('Message:', msg);
}

msg(); // Message: 🤡 <-- after 2 seconds
```

Multiple Promises

```
function who() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('🤡');
    }, 5000);
  });
}

function what() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('lurks');
    }, 300);
  });
}

function where() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('in the shadows');
    }, 500);
  });
}

async function msg() {
  const a = await who();
  const b = await what();
  const c = await where();

  //   const [a, b, c] = await Promise.all([who(), what(), where()]);


  console.log(`${ a } ${ b } ${ c }`);
}

msg();
```

-----

`Promise.all` returns an array with the resolved values once all the passed-in promises have resolved.

# Generators

Special kind of function with the ability to pause itself, and resume later,
allowing other code to run in the meantime.

Declare a generator function which returns generator objects g that can then be iterated using any of `Array.from(g), [...g], or for value of g loops`. 

```

function* generator () {
  yield 'f'
  yield 'o'
  yield 'o'
}

// * - Generators

```
When a generator contains `yield`
keyword, the execution is halted.


