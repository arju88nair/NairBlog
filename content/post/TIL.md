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


---
```
onomatopoeia
/ˌɒnə(ʊ)matəˈpiːə/

noun
the formation of a word from a sound associated with what is named (e.g. cuckoo, sizzle ).
the use of onomatopoeia for literary effect.
```

----

SQL vs NoSQL

 - SQL databases -  vertically scalable, which means that you can increase the load on a single server by increasing things like CPU, RAM or SSD. 
 
 - NoSQL databases -> are horizontally scalable. This means that you handle more traffic by sharding, or adding more servers in your NoSQL database.
 
  - NoSQL databases can ultimately become larger and more powerful, making NoSQL databases the preferred choice for large or ever-changing data sets.

  ---
## [Bits](https://web.stanford.edu/class/cs101/bits-bytes.html)


Number of bits and patterns

```
1 -	0 1

2 -	00 01 10 11

3 -	000 001 010 011
100 101 110 111
```

1 byte is group of 8 bits

8 bits can make 256 different patterns 

`2^n`

1 byte is enough to hold about 1 typed character, e.g. 'b' or 'X' or '$' 

Each letter is stored in a byte

100 typed letters takes up 100 bytes 

Adding in binary is just like normal addition with carrying

But when you run out of bits you can't carry anymore

Leftmost bit indicates sign, so carrying to the leftmost bit changes a number ffrom positive to negative.

So adding 1 to 2147483647 goes to -2147483648!
Called Integer Overflow


----

HTMLPurifier library to prevent attacks by cleaning html


- `mysql_real_escape_string` used when insert into database
- `htmlentities()` used when outputting data into webpage
- `htmlspecialchars()`  is roughly the same as htmlentities. The difference: character encodings.

  Both encode control characters like <, >, & and so on used for opening tags etc. htmlentities also encode chars from other languages like umlauts, euro-symbols and such. If your websites are UTF, use htmlspecialchars(), otherwise use htmlentities().

-  `strip_tags() ` - 

      htmlspecialchars / entities encode the special chars, so they're displayed but not interpreted. strip_tags REMOVES them. 
- `addslashes() ` - Returns a string with backslashes before characters that need to be quoted in database queries etc. These characters are single quote ('), double quote ("), backslash () and NUL (the NULL byte).

