---
title: "Dependency Injection"
date: 2018-11-14T12:47:21+05:30
draft: false
tags : [
    "PHP",
    "PHP7",
    "Interview"
   ]
---

Dependency injection is a technique whereby one object supplies the dependencies of another object

```
class Profile {
    public function deactivateProfile(Setting $setting)
    {
        $setting->isActive = false;
    }
}

```

# Advantages

-  Decoupling
Their purpose is isolated and can easily be swapped out by other components later. This way your code will be cleaner and decoupled.

-  Reusable code
Another advantage of dependency injection is that your code will be more reusable since there are no direct dependencies on other entities (objects or classes) in your code.

- Testable code

---


Classic PHP code 
## Here is how a code not using DI will roughly work:

Application needs Foo (e.g. a controller), so:
- Application creates Foo
- Application calls Foo
    - Foo needs Bar (e.g. a service), so:
    - Foo creates Bar
    - Foo calls Bar
        - Bar needs Bim (a service, a repository, …), so:  
        - Bar creates Bim
        - Bar does something


## Using dependency injection 

- Application needs Foo, which needs Bar, which needs Bim, so:
- Application creates Bim
- Application creates Bar and gives it Bim
- Application creates Foo and gives it Bar
- Application calls Foo
    - Foo calls Bar
    - Bar does something
    
This is the pattern of Inversion of Control. The control of the dependencies is inverted from one being called to the one calling.

The main advantage: the one at the top of the caller chain is always you. You can control all dependencies and have complete control over how your application works. You can replace a dependency by another (one you made for example).

For example what if Library X uses Logger Y and you want to make it use your logger Z? With dependency injection, you don't have to change the code of Library X.

Using a container #
Now how does a code using PHP-DI works:

Application needs Foo so:
Application gets Foo from the Container, so:
Container creates Bim
Container creates Bar and gives it Bim
Container creates Foo and gives it Bar
Application calls Foo
Foo calls Bar
Bar does something
In short, the container takes away all the work of creating and injecting dependencies.

Understanding with an example #
This is a real life example comparing a classic implementation (using new or singletons) VS using dependency injection.

----

```
class User 
{
    private $database = null;

    public function __construct() {
        $this->database = new database('host', 'user', 'pass', 'dbname');
    }

    public function getUsers() {
        return $this->database->getAll('users');
    }
}

$user = new User();
$user->getUsers();
```

This code again has these problems:

- The class User has implicit dependency on the specific database.This defeats Dependency inversion principle

- If we wanted to change database credentials, we need to edit the User class 

- What if we need to change the DB?

- The User class does not necessarily need to know about database connection, it should be confined to its own functionality only.This defeats the Single responsibility principle.

- It would become harder to write unit tests for the User class because we are instantiating the database class inside its constructor 

## Enter DI

```
class User 
{
    private $database = null;

    public function __construct(Database $database) {
        $this->database = $database;
    }

    public function getUsers() {
        return $this->database->getAll('users');
    }
}

$database = new Database('host', 'user', 'pass', 'dbname');
$user = new User($database);
$user->getUsers();

```

## IoC (Inversion of Control) 
 is all about relationship between higher level classes and detail classes. Higher level classes shouldn't depend on detail classes, but rather the contrary.