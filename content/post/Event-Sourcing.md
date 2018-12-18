---
title: "Event Sourcing"
date: 2018-12-18T09:42:13+05:30
draft: false
tags : [
    "Event Sourcing",
    "Tidbits"
]
---
> References 
[1](https://dev.to/barryosull/event-sourcing-what-it-is-and-why-its-awesome), [2](https://www.phproundtable.com/episode/event-sourcing-in-php)



>Instead of focussing on current state, you focus on the changes that have occurred over time. 

Thinking of application state as a frames in a video, we could "scrub" through different states of the application.

Every time something happens that is relevant, you just record what it was, then you tie to it, any extra details that are really necessary to understand what happened. Then later you can turn those events into state, by running one after another to see how they stack up.

So basically it's recording what happened, then generating state from those records.

---

Example using Shopping cart

Event
1. Shopping Cart Created
2. Item Added to Cart
3. Item Added to Cart
4. Item Removed from Cart
5. Shopping Cart Checked-Out


### Enforcing rules

Checking if the cart contains the item

 Check that an "Item Added to Cart" event has happened for that item, then you know the item is in the cart and that it can be removed.

 So, replay a subset of the events to get the answer you need. Called projecting the events, and the end result is a "projection".


 ----

 CRUD are not a suitable candidate for ES. Data mining , where you are looking to see behavior over time to influence marketing. Legal requirements.


 Event Sourcing will have an id (usually UUID) and a field to indicate which order the events happened.
 Often  Meta data as well. The Action is the first class citizen and the Data is the second class citizen.


For a huge amount of data -> Snapshot, a recent event which will be used to trace 
after it

---

### CQRS - Command Query Responsibility Segregation

> Plumbing for Event Sourcing.

 Is to have separate models for different purposes


   You generally start with a simple Command object, that then gets passed on to a Command Bus, that then figures out the CommandHandler, that then figures out which Object you actually want to change and passes the data from the Command to the actual Object. The actual Object is the one that is going to contain the data or raise the proper events.


   ----

  [Event sourcing DB](https://eventstore.org)