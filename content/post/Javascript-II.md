---
title: "Javascript II"
date: 2018-12-10T14:44:59+05:30
draft: false
tags : [
    "Javascript",
    "Interview",
   ]
---
>JavaScript engine is single threaded so the language itself is synchronous and hence blocking in nature

## [Event Loops](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

Not in the v8 source

Single threaded language - single call stack

Async is non blocking. So when a blocking setTimeOut is called, it's pushed to the `webapis` from the `stack` which are threaded.
When task is done,pushes to `task queue`. EL does one thing,if the stack from is `empty`, it pushes the thing from queue to stack

Same for xhr request making.

Timeout is not accurate. It's the minimum time for execution

Browser repaints `60fps`
Can't do render if there's anything in the stack.
Render got higher priority than Callbacks.

Render/repaints managed to get in between async


Provided by the environment where javascript is running which provides capability for asynchronous execution providing non-blocking functionality


In general, any function that does networking or uses timers to do things over a period of time will be asynchronous.

If the function takes a callback, you can look at what the callback is used for and usually it will be obvious whether is is asynchronous or not. If the function does not offer a callback, then it has no way of communicating asynchronous results so it is probably synchronous.


Using the File System module as an example, this is a synchronous file read:
```
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // blocks here until file is read
console.log(data);
// moreWork(); will run after console.log

 ```

And here is an equivalent asynchronous example:

```
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
  console.log(data);
});
// moreWork(); will run before console.log
```

`Libuv` ->Event loop for NodeJs


There is only one thread that executes JavaScript code and this is the thread where the event loop is running. The execution of callbacks is done by the event loop.

Libuv by default creates a thread pool with four threads to offload asynchronous work to. 

The event loop as a process is a set of phases with specific tasks that are processed in a round-robin manner.Not stacks or queues

---

# [Array methods](https://dev.to/frugencefidel/10-javascript-array-methods-you-should-know-4lk3)

##  forEach()

```
  const arr = [1, 2, 3, 4, 5, 6];

  arr.forEach(item => {
    console.log(item); // output: 1 2 3 4 5 6
  });

  ```
  ---

  ## includes()

This method check if array includes the item passed in the method.

  ```
  const arr = [1, 2, 3, 4, 5, 6];

  arr.includes(2); // output: true
  arr.includes(7); // output: false

```
---


## filter()

This method create new array with only elements passed condition inside the provided function.
```
  const arr = [1, 2, 3, 4, 5, 6];

  // item(s) greater than 3
  const filtered = arr.filter(num => num > 3);
  console.log(filtered); // output: [4, 5, 6]

  console.log(arr); // output: [1, 2, 3, 4, 5, 6]
  
  ```


  ---

 ##  map()

This method create new array by calling the provided function in every element.
```
  const arr = [1, 2, 3, 4, 5, 6];

  // add one to every element
  const oneAdded = arr.map(num => num + 1);
  console.log(oneAdded); // output [2, 3, 4, 5, 6, 7]

  console.log(arr); // output: [1, 2, 3, 4, 5, 6] 
  
  ```
  ---
## reduce()

The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value - MDN
```
  const arr = [1, 2, 3, 4, 5, 6];

  const sum = arr.reduce((total, value) => total + value, 0);
  console.log(sum); // 21


  ```
  ---


## some()

This method check if at least one of array's item passed the condition. If passed, it return 'true' otherwise 'false'.
```
  const arr = [1, 2, 3, 4, 5, 6];

  // at least one element is greater than 4?
  const largeNum = arr.some(num => num > 4);
  console.log(largeNum); // output: true

  // at least one element is less than or equal to 0?
  const smallNum = arr.some(num => num <= 0);
  console.log(smallNum); // output: false  

  ```

  ---


## every()

This method check if all array's item passed the condition. If passed, it return 'true' otherwise 'false'.
```
  const arr = [1, 2, 3, 4, 5, 6];

  // all elements are greater than 4
  const greaterFour = arr.every(num => num > 4);
  console.log(greaterFour); // output: false

  // all elements are less than 10
  const lessTen = arr.every(num => num < 10);
  console.log(lessTen); // output: true

  ```
  ----


 ## sort()

This method used to arrange/sort array's item either ascending or descending order.

  ```const arr = [1, 2, 3, 4, 5, 6];
  const alpha = ['e', 'a', 'c', 'u', 'y'];

  // sort in descending order
  descOrder = arr.sort((a, b) => a > b ? -1 : 1);
  console.log(descOrder); // output: [6, 5, 4, 3, 2, 1]

  // sort in ascending order
  ascOrder = alpha.sort((a, b) => a > b ? 1 : -1);
  console.log(ascOrder); // output: ['a', 'c', 'e', 'u', 'y']

  ```
  ---
## Array.from()

This change all thing that are array-like or iterable into true array especially when working with DOM, so that you can use other array methods like reduce, map, filter and so on.
```
  const name = 'frugence';
  const nameArray = Array.from(name);

  console.log(name); // output: frugence
  console.log(nameArray); // output: ['f', 'r', 'u', 'g', 'e', 'n', 'c', 'e']
working with DOM

  // I assume that you have created unorder list of items in our html file.

  const lis = document.querySelectorAll('li');
  const lisArray = Array.from(document.querySelectorAll('li'));

  // is true array?
  console.log(Array.isArray(lis)); // output: false
  console.log(Array.isArray(lisArray));  // output: true
  ```
---

## Array.of()

This create array from every arguments passed into it.

```  const nums = Array.of(1, 2, 3, 4, 5, 6);
  console.log(nums); // output: [1, 2, 3, 4, 5, 6]
  
  ```

  ---


  ## Functions

  ### Lambda => arrow function

  `const lambda = (a, b) => a + b;`


  ### First class functions

   >Can be used as a value of a variable.

   > That doesn’t accept other function as an argument and doesn’t return a function as its return value.

   ```
   const handler = () => console.log ('I am function');

document.addEventListener ('click', handler); 
```

### Higher-order function

> Accepts other function as an argument or returns a function as a return value.

```
const firstOrder = () => console.log ('First order strikes back!');

const higherOrder = whoStrikesBack => whoStrikesBack ();

higherOrder (firstOrder);

```

---
### Unary function 

> (i.e. monadic) is a function that accepts exactly one argument.


```
const unaryFunction = message => console.log (message);

const binaryFunction = (color, message) =>
  console.log (`%c${message}`, `color:${color}`);

const ternaryFunction = (fnc, color, message) =>
  fnc (`%c${message}`, `color:${color}`);

  ```


  ###  Pure function

> Where the return value is only determined by its arguments without any side effects.

>
  ---

  ## Currying

  > Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. 


  ```
const binaryFunction = (a, b) => a + b;

const curryUnaryFunction = a => b => a + b;

curryUnaryFunction (1); // returns a function: b => 1 + b

curryUnaryFunction (1) (2); // returns the number 3

```

`Push` function is impure itself and it alters the array it is called on and as such produces a side effect. The return value of push is a number index.

`Concat` on the other hand takes the array and concatenates it with the other array producing a whole new array without side effects.