---
title: "PHP7"
date: 2018-07-12T17:13:19+05:30
tags : [
    "PHP",
    "Interview",
    "OOP"
   ]
---

---------

# New to PHP 7
- New Zend engine
- Fast
- Facilitates Error Handling using exceptions
- 64-Bit Windows Systems Support
- New Spaceship and Null Coalescing Operators(<=> The spaceship operator returns 0 if both operands are equal, 1 if the left is greater, 
	and -1 if the right is greater. It’s also called a three-way comparison operator)

---



# PHP 7

- Scalar type declarations, has been introduced. Scalar type declaration has two options 
> coercive - coercive is default mode and need not to be specified.

```
	<?php
   function sum(int ...$ints) {
      return array_sum($ints);
   }
   print(sum(2, '3', 4.1));

```

> strict - strict mode has to explicitly hinted.


```
	<?php
   declare(strict_types=1);
   function sum(int ...$ints) {
      return array_sum($ints);
   }
   print(sum(2, '3', 4.1));
   //Error.Has to be int
   
```
