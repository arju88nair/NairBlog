---
title: "TIL"
date: 2019-01-22T15:38:32+05:30
draft: false
tags: ["TIL",
"Random"]
---
> Can't believe I am starting this post well after the blog which is name TIL

---
## [Hypermedia As The Engine Of Application State (HATEOAS)](https://en.wikipedia.org/wiki/HATEOAS)

> A client interacts with a network application whose application servers provide information dynamically through hypermedia

### Example

```
GET /accounts/12345 HTTP/1.1
Host: bank.example.com
Accept: application/xml
...
```
The response is:

```HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: ...

<?xml version="1.0"?>
<account>
    <account_number>12345</account_number>
    <balance currency="usd">100.00</balance>
    <link rel="deposit" href="https://bank.example.com/accounts/12345/deposit" />
    <link rel="withdraw" href="https://bank.example.com/accounts/12345/withdraw" /> 
    <link rel="transfer" href="https://bank.example.com/accounts/12345/transfer" />
    <link rel="close" href="https://bank.example.com/accounts/12345/status" />
</account>
```
The response contains these possible follow-up links: make a deposit, withdrawal, or transfer, or close the account.

When the account information is retrieved later, the account is overdrawn:
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: ...

<?xml version="1.0"?>
<account>
    <account_number>12345</account_number>
    <balance currency="usd">-25.00</balance>
    <link rel="deposit" href="https://bank.example.com/accounts/12345/deposit" />
</account>
```
Now only one link is available: to deposit more money. In its current state, the other links are not available. Hence the term  ` Engine of Application State`. The available actions varies as the state of the resource varies.
---
## API
  - Contract between applications
  - Following rules

---


## Synchronous programming 

### Single threaded
 
 - A thread is assigned to one task and starts working on it. Once the task completes then it is available for the next task. 
 - Cannot leave the executing task in mid to take up another task. 


### Multi-threaded
 -  Pool/multiple threads which can take up these tasks and start working on that.
 
 ### Asynchronous Programming Model
 – A thread once start executing a task it can hold it in mid, save the current state and start executing another task.
 - If our system is capable of having multiple threads then all the threads can work in asynchronous model as well
 
 ### Concurrency 
 - processing multiple requests at a time. 

