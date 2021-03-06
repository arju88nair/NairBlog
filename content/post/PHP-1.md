---
title: "PHP Part 1"
date: 2018-07-11T17:02:17+05:30
tags : [
    "PHP",
    "OOP",
    "Interview"
   ]
---

## One important principle of OOP is that a class should do one thing, and it should do it well.

---

- Polymorphism - which classes have different functionality while sharing a common interface.

- Implements to extend an interface in PM

- An interface is similar to a class except that it cannot contain code. An interface can define method names and arguments, but not the contents of the methods.A class can implement multiple interfaces.
An interface does not contain any code,it contain only declaration of methods,properties,events. Interfaces allow us to code which specifies which methods a class must have implement . Interfaces defines with the word interface . All methods in interfaces must be public

 ```  <?php
interface Shape {
   public function getArea();
}

class Square implements Shape {
   private $width;
   private $height;

   public function __construct($width, $height) {
      $this->width = $width;
      $this->height = $height;
   }

   public function getArea(){
      return $this->width * $this->height;
   }
}

class Circle implements Shape {
   private $radius;

   public function __construct($radius) {
      $this->radius = $radius;
   }

   public function getArea(){

      return 3.14 * $this->radius * $this->radius;
   }
}

function calculateArea(Shape $shape) {
   return $shape->getArea();
}

$square = new Square(5, 5);
$circle = new Circle(7);

echo calculateArea($square), "<br/>";
echo calculateArea($circle);
?>

```
___

- An abstract class is a mix between an interface and a class. It can define functionality as well as interface 
- Abstract classes look like interfaces.Abstract classes may contain code although it may also have abstract method that do not have code. Abstract classes defines only signature of the method ,not implementation. The child class which inherit the abstarct class must define all the abstarct methods of its parent class .

- Encapsulation - Packing of data and functions into a single component

- Singleton pattern in order to restrict the number of instances that can be created from a resource consuming class to only one.
Example: Database instantiation




- Class − This is a programmer-defined data type, which includes local functions as well as local data. 

- Object − An individual instance of the data structure defined by a class. You define a class once and then make many objects that belong to it. Objects are also known as instance.

- Inheritance − When a class is defined by inheriting existing function of a parent class then it is called inheritance. Here child class will inherit all or few member functions and variables of a parent class.

- Polymorphism − This is an object oriented concept where same function can be used for different purposes. For example function name will remain same but it make take different number of arguments and can do different task.

- Overloading − a type of polymorphism in which some or all of operators have different implementations depending on the types of their arguments. Similarly functions can also be overloaded with different implementation.

```
class overload {
    public $name;
    public function __construct($agr) {
        $this->name = $agr;
    }
    public function __call($methodname, $agrument) {
         if($methodname == 'sum2') {

          if(count($agrument) == 2) {
              $this->sum($agrument[0], $agrument[1]);
          }
          if(count($agrument) == 3) {

              echo $this->sum1($agrument[0], $agrument[1], $agrument[2]);
          }
        }
    }
    public function sum($a, $b) {
        return $a + $b;
    }
    public function sum1($a,$b,$c) {

        return $a + $b + $c;
    }
}
$object = new overload('Sum');
echo $object->sum2(1,2,3);
```

- Data Abstraction − Any representation of data in which the implementation details are hidden (abstracted).

- Encapsulation − refers to a concept where we encapsulate all the data and member functions together to form an object.

- Constructor − refers to a special type of function which will be called automatically whenever there is an object formation from a class.

- Destructor − refers to a special type of function which will be called automatically whenever an object is deleted or goes out of scope.


- Object interfaces allow you to create code which specifies which methods a class must implement, without having to define how these methods are handled.

  $this is a special variable and it refers to the same object ie. itself.

- Constructor Functions are special type of functions which are called automatically whenever an object is created.

```
function __construct( $par1, $par2 ) {
   $this->title = $par1;
   $this->price = $par2;
}
```

- Function definitions in child classes override definitions with the same name in parent classes. In a child class, we can modify the definition of a function inherited from parent class.

- An abstract class is one that cannot be instantiated, only inherited. You declare an abstract class with the keyword abstract

- Final keyword, which prevents child classes from overriding a method by prefixing the definition with final. If the class itself is being defined final then it cannot be extended.



- Overloading is defining functions that have similar signatures, yet have different parameters. Overriding is only pertinent to derived classes, where the parent class has defined a method and the derived class wishes to override that method.

- In PHP, you can only overload methods using the magic method __call.

```
- Overriding:


<?php

class Foo {
   function myFoo() {
      return "Foo";
   }
}

class Bar extends Foo {
   function myFoo() {
      return "Bar";
   }
}

$foo = new Foo;
$bar = new Bar;
echo($foo->myFoo()); //"Foo"
echo($bar->myFoo()); //"Bar"
?>

```
-------------

- If the file is not found by require(), it will cause a fatal error and halt the execution of the script. If the file is not found by include(), a warning will be issued, but execution will continue.

- require() includes and evaluates a specific file, while require_once() does that only if it has not been included before (on the same page). So, require_once() is recommended to use when you want to include a file where you have a lot of functions for example. This way you make sure you don’t include the file more times and you will not get the “function re-declared” error.

- Sessions are stored on the server, and cookies (A cookie is often used to identify a user) are stored on the user’s computers in the text file format. 
```
Setcookie(“sample”, “ram”, time()+3600); 
echo $_COOKIE[“user”]
```
```
mysql_select_db($db_name);
$my_qry = mysql_query(“SELECT * FROM `users` WHERE `u_id`=’1′; “); 
$result = mysql_fetch_array($my_qry);
echo $result[‘First_name’];
mysql_fetch_row
mysql_fetch_array
mysql_fetch_object
mysql_fetch_assoc
```
```
array explode ( string $delimiter , string $string [, int $limit ] ); 
```
This function breaks a string into an array.
```
header(“Location:index.php”);
```

- mysql_fetch_assoc function Fetch a result row as an associative array, While mysql_fetch_array() fetches an associative array, a numeric array, or both

- The enctype attribute determines how the form-data should be encoded when submitting it to the server. We need to set enctype as “multipart/form-data”when we are using a form for uploading files.


- Object orientation is a software/Web development methodology that is based on the modeling a real world system.An object is the core concept involved in the object orientation. An object is the copy of the real world enity.

 - if $var contains “message”, $$var is the same as $message.

- unset() sets a variable to “undefined” while unlink() deletes a file we pass to it from the file system.

```

$a = '1';
$b = &$a;
$b = "2$b";
echo $a.", ".$b; 21,21
```


- GET displays the submitted data as part of the URL, during POST this information is not shown as it’s encoded in the request.
- GET can handle a maximum of 2048 characters, POST has no such restrictions.
- GET allows only ASCII data, POST has no restrictions, binary data are also allowed.
- Normally GET is used to retrieve data while POST to insert and update.

```
ini_set('display_errors', 1)  error_reporting(E_ALL)
```
---

- Traits are a mechanism that allows you to create reusable code in languages like PHP where multiple inheritance is not supported. A Trait cannot be instantiated on its own.


```
<?php
trait Sharable {

public function share($item)  
{  
return ‘share this item’;  
}

}  

class Post {

use Sharable;

}

class Comment {

use Sharable;

}  

$post = new Post;  
echo $post->share(”); // ‘share this item’

$comment = new Comment;  
echo $comment->share(”); // ‘share this item’  

```
--

- An Abstract Class is basically a blueprint that should only ever be extended by child classes and not used directly. 

- Private – Visible only in its own class
- Public – Visible to any other code accessing the class
- Protected – Visible only to classes parent(s) and classes that extend the current class

- Getters and setters are methods used to declare or obtain the values of variables, usually private ones.

---

- The controller handles data passed to it by the view and also passes data to the view. It’s responsible for interpretation of the data sent by the view and dispersing that data to the appropriate models awaiting results to pass back to the view. Very little, if any business logic should be occurring in the controller.

- The model’s job is to handle specific tasks related to a specific area of the application or functionality. Models will communicate directly with your database or other storage system and will handle business logic related to the results.

- The view is passed data by the controller and is displayed to the user.

---

- To prevent SQL injections, one should always check & escape all user input
mysqli_*

```
$i = 016;
echo $i / 2;
```

- The Output should be 7. The leading zero indicates an octal number in PHP, so the number evaluates to the decimal number 14 instead to decimal 16.

- PSRs are PHP Standards Recommendations that aim at standardising common aspects of PHP Development.


- Using Composer is a tool for dependency management. The candidate can declare the libraries your product relies on and Composer will manage the installation and updating of the libraries.



```
<?php
class MyClass {
  private $firstField;
  private $secondField;

  public function __get($property) {
    if (property_exists($this, $property)) {
      return $this->$property;
    }
  }

  public function __set($property, $value) {
    if (property_exists($this, $property)) {
      $this->$property = $value;
    }

    return $this;
  }
}
?>
```

- Use an interface when you want to force developers working in your system (yourself included) to implement a set number of methods on the classes they'll be building.

- Use an abstract class when you want to force developers working in your system (yourself included) to implement a set numbers of methods and you want to provide some base methods that will help them develop their child classes.


- Java (interpreted) and C (or C++) (compiled) might have been a better example. Basically, compiled code can be executed directly by the computer’s CPU. The code of interpreted languages however must be translated at run-time from any format to CPU machine instructions. This translation is done by an interpreter.

- undefined means a variable has been declared but has not yet been assigned a value. On the other hand, null is an assignment value.

- Wrapping some data in single unit is called Encapsulation. Second advantage of encapsulation is you can make the class read only or write only by providing setter or getter method

- If the value of the argument within the function is changed, it does not get changed outside of the function)

>htmlentities() - XSS
mysql_real_escape_string - SQLi
Token -CSRF


- A static method is accessible without needing instantiation of a class. It means there is no need to make an object to call the static methods  Scope resolution operator

- Dependency injection is a fancy phrase that essentially means this: class dependencies are "injected" into the class via the constructor or, in some cases, "setter" methods.

------------------



## Design Patterns


### Singleton Pattern
> A Class has one instance, It provides a global access point to it, Following code will explain about singleton concept.


Shared resources. , a database class, a template class, and a global variable depot class. All have to be shared by all modules/classes that are being used throughout the code. 

Logging is a specific example of an "acceptable" Singleton because it doesn't affect the execution of your code.
```
<?php
   class Singleton {
      public static function getInstance() {
         static $instance = null;
         
         if (null === $instance) {
            self::$instance = new __CLASS__;    
                 }
         return self::$instance;
      }
      protected function __construct() {
      }
      
      private function __clone() {
      }
      
      private function __wakeup() {
      }
   }
   
   class SingletonChild extends Singleton {
   }
   
   $obj = Singleton::getInstance();
   var_dump($obj === Singleton::getInstance());
   
   $anotherObj = SingletonChild::getInstance();
   var_dump($anotherObj === Singleton::getInstance());
   var_dump($anotherObj === SingletonChild::getInstance()); 
?>
```



    - Debug Logging: Almost all developers will agree that a way to debug logging should be available for every function and part of the code. A singleton could serve this purpose without harming readability, testability or maintainability.

    - Filesystem and Database Access: The argument can be made for Singletons proving access to the filesystem and database, now this might work if you need a single global filesystem or database access point it trades flexibility and testability for modicum amount of convenience.



### Factory

> A Class Simple Creates the object and you want to use that object
```
<?php
   class Automobile {
      private $bikeMake;
      private $bikeModel;
      
      public function __construct($make, $model) {
         $this->bikeMake = $make;
         $this->bikeModel = $model;
      }
      
      public function getMakeAndModel() {
         return $this->bikeMake . ' ' . $this->bikeModel;
      }
   }
   
   class AutomobileFactory {
      public static function create($make, $model) {
         return new Automobile($make, $model);
      }
   }
   
   $pulsar = AutomobileFactory::create('ktm', 'Pulsar');
   print_r($pulsar->getMakeAndModel());
   
?>
```

### Strategy pattern

> Makes a family algorithm and encapsulates each algorithm. 
```
<?php
   $elements = array(
      array(
         'id' => 2,
         'date' => '2011-01-01',
      ),
      array(
         'id' => 1,
         'date' => '2011-02-01'
      )
   );
   
   $collection = new ObjectCollection($elements);
   
   $collection->setComparator(new IdComparator());
   $collection->sort();
   
   echo "Sorted by ID:\n";
   print_r($collection->elements);
   
   $collection->setComparator(new DateComparator());
   $collection->sort();
   
   echo "Sorted by date:\n";
   print_r($collection->elements);
?>

```

### Abstract factory

>An abstract factory defines what objects the non-abstract or concrete factory will need to be able to create. 