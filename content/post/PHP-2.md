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
 
 ---



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

--------------

## Coroutines

Coroutines add to the above functionality is the ability to send values back to the generator. This turns the one-way communication from the generator to the caller into a two-way channel between the two.

Values are passed into the coroutine by calling its ->send() method instead of ->next(). 

```
function logger($fileName) {
    $fileHandle = fopen($fileName, 'a');
    while (true) {
        fwrite($fileHandle, yield . "\n");
    }
}

$logger = logger(__DIR__ . '/log');
$logger->send('Foo');
$logger->send('Bar');

```

Here yield isn’t used as a statement here, but as an expression, i.e. it has a return value. The return value of yield is whatever was passed to ->send(). 

---------
## Closures
A closure is an anonymous function that can access variables imported from the outside scope without using any global variables.

A Lambda is an anonymous function that can be assigned to a variable or passed to another function as an argument.

```
// Anonymous function  
 // assigned to variable  
 $greeting = function () {  
 return "Hello world";  
 }

// Call function  
 echo $greeting();  
 // Returns "Hello world"   

```

 Closures are more or less Lambdas.

 ```
 // Create a user  
$user = "Philip";

// Create a Closure  
$greeting = function() use ($user) {  
echo "Hello $user";  
};

// Greet the user  
$greeting(); // Returns "Hello Philip" 
```
 Closure is able to access the $user variable. because it was declared in the use clause of the Closure function definition.

 If you were to alter the $user variable within the Closure, it would not effect the original variable. To update the original variable, we can append an ampersand. An ampersand before a variable means this is a reference and so the original variable is also updated.


 ```
 // Set counter  
$i = 0;  
// Increase counter within the scope  
// of the function  
$closure = function () use ($i){ $i++; };  
// Run the function  
$closure();  
// The global count hasn’t changed  
echo $i; // Returns 0

// Reset count  
$i = 0;  
// Increase counter within the scope  
// of the function but pass it as a reference  
$closure = function () use (&$i){ $i++; };  
// Run the function  
$closure();  
// The global count has increased  
echo $i; // Returns 1  
```

```
// Set a multiplier  
 $multiplier = 3;

// Create a list of numbers  
 $numbers = array(1,2,3,4);

// Use array_walk to iterate  
 // through the list and multiply  
 array_walk($numbers, function($number) use($multiplier){  
 echo $number * $multiplier;  
 });

 ```


Real life scenarios

```
Route::get(‘user/(:any)’, function($name){  
return "Hello " . $name;  
});  

```

## __construct

```
class Entity {

protected $meta;

public function __construct(array $meta)  
{  
$this->meta = $meta;  
}

}

class Tweet extends Entity {

protected $id;  
protected $text;

public function __construct($id, $text, array $meta)  
{  
$this->id = $id;  
$this->text = $text;

parent::__construct($meta);  
}

}  

```

------


## Namespace
One library’s PHP code might use the same class name as another. When both libraries are used in the same namespace, they collide and cause trouble.Two files with the same name may co-exist in separate directories. Likewise, two PHP classes with the same name may co-exist in separate PHP namespaces. 

It allows you to use the same function or class name in different parts of the same program without causing a name collision.
---
## Namespaces

Namespacing does for functions and classes what scope does for variables. It allows you to use the same function or class name in different parts of the same program without causing a name collision

> Namespace as a person's surname


```
namespace MyProject;

function output() {
    # Output HTML page
    echo 'HTML!';
}

namespace RSSLibrary;

function output(){
    # Output RSS feed
    echo 'RSS!';
}

\MyProject\output();
\RSSLibrary\output();

```

----

## Buffer

 *_clean variants just empty the buffer, whereas *_flush functions print what is in the buffer (send the contents to the output buffer).
Example:

```
ob_start();
print "foo";      // This never prints because ob_end_clean just empties
ob_end_clean();   //    the buffer and never prints or returns anything.

ob_start();  // Turns on
print "bar";      // This IS printed, but just not right here.
ob_end_flush();   // It's printed here, because ob_end_flush "prints" what's in
                  // the buffer, rather than returning it
                  //     (unlike the ob_get_* functions)

```


> If outbut buffering is still active when the script ends, PHP outputs it automatically. In effect, every script ends with ob_end_flush()

 `ob_get_contents ( void ) : string` -  Gets the contents of the output buffer without clearing it. 


 ----

 ## PHP server mods and such

### Apache Module (mod_php)

- PHP interpreter is embedded in each Apache process that’s spawned on the server. 
-  No need to deal with any external process unlike CGI or FastCGI
- Good for apps like Wordpress etc where they deal with many requests contain PHP codes
-  Larger footprint



### FastCGI

- External interpreter
-  PHP scripts with FastCGI, each request is passed from the web server to FastCGI via a communication socket. 
- Cannot use PHP directives in .htaccess. 
- Improved security as PHP code execution is isolated from web server.
- Static content will not be processed by PHP interpreter.

### FastCGI Process Manager (FPM) 
 
 - Advanced FastCGI with better features



 ----
 ## Request Lifecycle 



 - Apache gets the request
 -  Search for `index.php`
 -  Sends the file to the interpreter
 - Does the stuff and returns the response to the server
 -  Displays the response in the browser