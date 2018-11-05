---
title: "Promises"
date: 2018-11-02T11:14:30+05:30
draft: true
---

# Promises

Promises -  “a proxy for a value that will eventually become available”. 


---------


## Async
The async function declaration defines an asynchronous function, which returns an AsyncFunction object.

```
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  var result = await resolveAfter2Seconds();
  console.log(result);
  // expected output: 'resolved'
}

asyncCall();

```


An async function can contain an await expression that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution and returns the resolved value.