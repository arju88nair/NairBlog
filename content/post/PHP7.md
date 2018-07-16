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
- Scalar type declarations, has been introduced. Scalar type declaration has two options −
coercive - coercive is default mode and need not to be specified.
```
	<?php
   // Coercive mode
   function sum(int ...$ints) {
      return array_sum($ints);
   }
   print(sum(2, '3', 4.1));

```
- strict - strict mode has to explicitly hinted.

```
	<?php
   // Strict mode
   declare(strict_types=1);
   function sum(int ...$ints) {
      return array_sum($ints);
   }
   print(sum(2, '3', 4.1));
   //Error.Has to be int
   
```

---

- Return type declarations has been introduced. Return type declaration specifies the type of value that a function should return.
```
declare(strict_types = 1);
   function returnIntValue(int $value): int {
      return $value;
   }
   print(returnIntValue(5));
```
   

---

- Null coalescing operator (??). Terinary operator with isset()
 
 ```
 $username = $_GET['username'] ?? 'not passed';
 
 // Equivalent code using ternary operator
 $username = isset($_GET['username']) ? $_GET['username'] : 'not passed';
```
---

- Anonymous classes can now be defined using new class. Anonymous class can be used in place of a full class definition.

```
<?php
   interface Logger {
      public function log(string $msg);
   }

   class Application {
      private $logger;

      public function getLogger(): Logger {
         return $this->logger;
      }

      public function setLogger(Logger $logger) {
         $this->logger = $logger;
      }  
   }

   $app = new Application;
   $app->setLogger(new class implements Logger {
      public function log(string $msg) {
         print($msg);
      }
   });

   $app->getLogger()->log("My first Log Message");
?>
```
---

- Closure::call() method is added as a shorthand way to temporarily bind an object scope to a closure and invoke it.

```
<?php
   class A {
      private $x = 1;
   }

   // Define a closure Pre PHP 7 code
   $getValue = function() {
      return $this->x;
   };

   // Bind a clousure
   $value = $getValue->bindTo(new A, 'A'); 

   print($value());
?>
It produces the following browser output −
1

```
> PHP7
```
<?php
   class A {
      private $x = 1;
   }

   // PHP 7+ code, Define
   $value = function() {
      return $this->x;
   };

   print($value->call(new A));
?>
```
