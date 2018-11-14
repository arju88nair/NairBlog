---
title: "Javascript"
date: 2018-07-22T13:50:50+05:30
tags : [
    "Javascript",
    "Interview",
   ]
---

## Callback functions
-------------------

They are derived from a programming paradigm known as functional programmings

A callback function, also known as a higher-order function, is a function that is passed to another function
Eg:

``` 

$("#btn_1").click(function() {
  alert("Btn 1 Clicked");
});

```



Functional programming (often abbreviated FP) is the process of building software by composing pure functions, avoiding shared state, mutable data, and side-effects

A pure function is a function which:
Given the same inputs, always returns the same output, and
Has no side-effects


Shared state is any variable, object, or memory space that exists in a shared scope, or as the property of an object being passed between scopes.


---------
(https://developers.google.com/web/updates/2015/03/introduction-to-fetch#response_types)
An XMLHttpRequest would need two listeners to be set to handle the success and error cases and a call to open() and send(). 

```
function reqListener() {
  var data = JSON.parse(this.responseText);
  console.log(data);
}

function reqError(err) {
  console.log('Fetch Error :-S', err);
}

var oReq = new XMLHttpRequest();
oReq.onload = reqListener;
oReq.onerror = reqError;
oReq.open('get', './api/some.json', true);
oReq.send();

```

Replaces with
```

fetch('./api/some.json')
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' +
          response.status);
        return;
      }

      // Examine the text in the response
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error :-S', err);
  });

```

 > Types

 ```
fetch('users.json').then(function(response) {
    console.log(response.headers.get('Content-Type'));
    console.log(response.headers.get('Date'));

    console.log(response.status);
    console.log(response.statusText);
    console.log(response.type);
    console.log(response.url);
});
```

Gives response.type of "basic", "cors" or "opaque". 

When a request is made for a resource on the same origin, the response will have a basic type and there aren't any restrictions on what you can view from the response.

If a request is made for a resource on another origin which returns the CORs headers, then the type is cors. cors and basic responses are almost identical except that a cors response restricts the headers you can view to `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`, and `Pragma`.
An opaque response is for a request made for a resource on a different origin that doesn't return CORS headers. With an opaque response we won't be able to read the data returned or view the status of the request, meaning we can't check if the request was successful or not.

> POST
```
fetch(url, {
    method: 'post',
    headers: {
      "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"
    },
    body: 'foo=bar&lorem=ipsum'
  })
  .then(json)
  .then(function (data) {
    console.log('Request succeeded with JSON response', data);
  })
  .catch(function (error) {
    console.log('Request failed', error);
  });

```

  > Example
  ```
    function createNode(element) {
      return document.createElement(element);
  }

  function append(parent, el) {
    return parent.appendChild(el);
  }

  const ul = document.getElementById('authors');
  const url = 'https://randomuser.me/api/?results=10';
  fetch(url)
  .then((resp) => resp.json())
  .then(function(data) {
    let authors = data.results;
    return authors.map(function(author) {
      let li = createNode('li'),
          img = createNode('img'),
          span = createNode('span');
      img.src = author.picture.medium;
      span.innerHTML = `${author.name.first} ${author.name.last}`;
      append(li, img);
      append(li, span);
      append(ul, li);
    })
  })
  .catch(function(error) {
    console.log(JSON.stringify(error));
  });   

  ```

-----------
A callback is a function that is to be executed after another function (normally asynchronous) has finished executing — hence the name ‘call back’.

(https://javascript.info/callbacks)

Most of the JS functions are asynchronous
```

function loadScript(src) {
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}

loadScript('/my/script.js'); // the script has "function newFunction() {…}"
newFunction(); // no such function!
Will fail
```


So we add callbacks
```
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(script);

  document.head.append(script);
}

Now if we want to call new functions from the script, we should write that in the callback:

loadScript('/my/script.js', function() {
  // the callback runs after the script is loaded
  newFunction(); // so now it works
  ...
});

```
```

function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;
  script.onload = () => callback(script);
  document.head.append(script);
}

loadScript('https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js', script => {
  alert(`Cool, the ${script.src} is loaded`);
  alert( _ ); // function declared in the loaded script
});
```


Here, after the script.onload, callback is loaded witht eh argument script.


> Error handling
```
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`Script load error for ${src}`));

  document.head.append(script);
}

```
---------------

let works similarly to var, but the variable it declares is block-scoped, it only exists within the current block. var is function-scoped.

```
function order(x, y) {
    if (x > y) { // (A)
        let tmp = x;
        x = y;
        y = tmp;
    }
    console.log(tmp===x); // ReferenceError: tmp is not defined
    return [x, y];
}

```
const works like let, but the variable you declare must be immediately initialized, with a value that can’t be changed afterwards.

```
const foo;
    // SyntaxError: missing = in const declaration

const bar = 123;
bar = 456;
    // TypeError: `bar` is read-only

```

In contrast, var-declared variables are function-scoped:
```
function func() {
    if (true) {
        var tmp = 123;
    }
    console.log(tmp); // 123
}
```

-----------------
(http://exploringjs.com/es6/ch_arrow-functions.html)

## Arrow function

```
const arr = [1, 2, 3];
const squares = arr.map(x => x * x);

// Traditional function expression:
const squares = arr.map(function (x) { return x * x });

--------------
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
let user = {
  name: "John",
  age: 30,
  "likes birds": true  // multiword property name must be quoted
};
```
------------
The main concept of memory management in JavaScript is reachability.

----------------
This

```
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("Hello!");
};

user.sayHi(); // Hello!

```
It’s common that an object method needs to access the information stored in the object to do its job.

```
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(this.name);
  }

};

user.sayHi(); // John

```
-----------

> jQuery .live()
Attach an event handler for all elements which match the current selector, now and in the future.

> jQuery .on()
Attach an event handler function for one or more events to the selected elements.

```
$(function () {
    $("#container a").bind("click", function () {
        console.log("clicked");
    });
});

```
When you are calling bind() , you are attaching an event handler to every single matched element in the selection, in our case every anchor element in the div ‘container’.

The same code can also be written using click() which is a shorthand way of writing bind().

```
$("#container a").click(function () {
    console.log("clicked");
});
```


```
$(function () {
    $("#container a").live("click", function () {
        console.log("clicked");
    });
});
```
live() implements event delegation. The handler bound to live() is not bound to the anchor element, as it may so appear. Instead live() binds a handler to the root of the DOM. So rather than attaching 100’s of event handlers to all the anchor elements in the ‘container’ div, using live() attaches just one event handler to the root document, along with the associated selector (in our case #container a) and event information.


```
$('#click li').click(function() {
    $(this).parent().append($('<li>List item</li>'));
});
    
    
$('#on').on('click', 'li', function() {
    $(this).parent().append($('<li>List item</li>'));
});

``` 

Here, the newly created li s won't have the click listener for the click method


---------------

Class Inheritance: A class is like a blueprint — a description of the object to be created. Classes inherit from classes can create subclass relationships

Prototypal Inheritance: A prototype is a working object instance. Objects inherit directly from other objects.
Class objects have a property called `prototype`, which is also an object.

-----------

