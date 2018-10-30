---
title: "PHP Part 2"
date: 2018-07-16T13:14:11+05:30
tags : [
    "PHP",
    "OOP",
    "Interview"
   ]
---

## Error Control Operators 
> @ -  Suppresses errors

## extract()
> It converts array keys into variable names and array values into variable value. 

```
 // input array
    $state = array("AS"=>"ASSAM", "OR"=>"ORRISA", "KR"=>"KERELA");
     
    extract($state);
     
    // after using extract() function
    echo"\$AS is $AS\n\$KR is $KR\n\$OR is $OR";
    
    
 ------
 $AS is ASSAM
 $KR is KERELA
 $OR is ORRISA
 
```

## Autoload

Every time you want to use a new class in your PHP project, first you need to include this class . However if you have __autoload function defined, inclusion will handle itself.

```
// Without autoload
include "classes/class.Foo.php";
 
$foo = new Foo;
$foo->start();
$foo->stop();
```

```
// By autload
function __autoload($class_name) 
{
    require_once $DOCUMENT_ROOT.“classes/class.”.$class_name.“.php”;
}
 
$foo = new Foo;
$foo->start();
$foo->stop();
```

---
 > A closure is good when you want a local function that's only used for some small, specific purpose.
 
 ```
 function replace_spaces ($text) {
     $replacement = function ($matches) {
         return str_replace ($matches[1], ' ', '&nbsp;').' ';
     };
     return preg_replace_callback ('/( +) /', $replacement, $text);
 }
 
 ```
 This lets you define the replacement function locally inside replace_spaces(), so that it's not:
 1) Cluttering up the global namespace
 2) Making people three years down the line wonder why there's a function defined globally that's only used inside one other function
 
## [S.O.L.I.D. STANDS FOR : ](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
  -  S — Single responsibility principle
  > A class should have one and only one reason to change, meaning that a class should only have one job.
  -  O — Open closed principle
  > Objects or entities should be open for extension, but closed for modification.
   - L — Liskov substitution principle
   > Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.
  -  I — Interface segregation principle
  > A client should never be forced to implement an interface that it doesn't use or clients shouldn't be forced to depend on methods they do not use.
  -  D — Dependency Inversion principle
  > ntities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.
 
 --------


 ## Generators

 Generators provide an easy way to implement simple iterators without the overhead or complexity of implementing a class that implements the Iterator interface.

 A generator allows you to write code that uses foreach to iterate over a set of data without needing to build an array in memory

 ```
 function xrange($start, $end, $step = 1) {
    for ($i = $start; $i <= $end; $i += $step) {
        yield $i;
    }
}

foreach (xrange(1, 1000000) as $num) {
    echo $num, "\n";
}
```


 Generators are interruptible functions, where the yield statements constitute the interruption points.

 In above example, if you call xrange(1, 1000000) no code in the xrange() function is actually run. Instead PHP just returns an instance of the Generator class which implements the Iterator interface:


 The code is only run once you invoke one of the iterator methods on the object. E.g. if you call $range->rewind() the code in the xrange() function will be run until the first occurrence of yield in the control flow. In this case it means that $i = $start and then yield $i are run. Whatever was passed to the yield statement can then be fetched using $range->current()
 

To continue executing the code in the generator you need to call the $range->next() method. This will again resume the generator until a yield statement is hit. Thus, using a succession of ->next() and ->current() calls, you can get all values from the generator, until at some point no yield is hit anymore.