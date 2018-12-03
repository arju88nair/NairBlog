---
title: "Laravel"
date: 2018-07-20T18:08:33+05:30
tags : [
    "PHP",
    "Interview",
    "Laravel"
   ]
---
LifeCycle

> "bootstrapped"? In general, means registering things, including registering service container bindings, event listeners, middleware, and even routes.

 

`index.php`

- Loads the Composer generated autoloader definition, and then retrieves an instance of the Laravel application from bootstrap/app.php script. The first action taken by Laravel itself is to create an instance of the application 

`HTTP / Console Kernels`

- The incoming request is sent to either the HTTP kernel or the console kernel, depending on the type of request that is entering the application

- It extends the illuminate\Foundation\Http\Kernel class, which defines an array of bootstrappers that will be run before the request is executed. These bootstrappers configure error handling, configure logging, detect the application environment, and perform other tasks that need to be done before the request is actually handled.

- Also defines a list of HTTP middleware that all requests must pass through before being handled by the application. These middleware handle reading and writing the HTTP session, determining if the application is in maintenance mode, verifying the CSRF token, and more.


`Service Providers`

- Important Kernel bootstrapping .
- Configured in `config/app.php`
- Responsible for bootstrapping all of the framework's various components, such as the database, queue, validation, and routing components

`Dispatch Request`

- Once the application has been bootstrapped and all service providers have been registered, the  Request will be handed off to the router for dispatching. The router will dispatch the request to a route or controller, as well as run any route specific middleware.

> index.php -> bootstrap/app.php(instance from autoload of composer) -> HTTP/Console kernel(bootstrap/app.php) -> Loads the application instance-> loads request, response and all sufficient interfaces - > -> Dispatcher
---

 > The application instance is created, the service providers are registered, and the request is handed to the bootstrapped application. It's really that simple!

-------

`Service container`
 -  Is a powerful tool for managing class dependencies and performing dependency injection. Dependency injection is a fancy phrase that essentially means this: class dependencies are "injected" into the class via the constructor or, in some cases, "setter" methods.


`Facades` 
- Provides a "static" interface to classes that are available in the application's service container. 

----
- The Illuminate\Support\Collection class provides a fluent, convenient wrapper for working with arrays of data. 
```
$collection = collect(['taylor', 'abigail', null])->map(function ($name) {
    return strtoupper($name);
})
->reject(function ($name) {
    return empty($name);
});
```



## Accessors and Mutators
- Accessors and mutators allow you to format Eloquent attribute values when you retrieve or set them on model instances.

- The accessor will automatically be called by Eloquent when attempting to retrieve the value of the first_name attribute:
```
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * Get the user's first name.
     *
     * @param  string  $value
     * @return string
     */
    public function getFirstNameAttribute($value)
    {
        return ucfirst($value);
    }
}
```

> Mutator
```
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * Set the user's first name.
     *
     * @param  string  $value
     * @return void
     */
    public function setFirstNameAttribute($value)
    {
        $this->attributes['first_name'] = strtolower($value);
    }
}

```
- When building JSON APIs, you will often need to convert your models and relationships to arrays or JSON. 
> return $user->toArray();
> return $user->toJson();

---