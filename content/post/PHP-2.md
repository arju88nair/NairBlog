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
 

 