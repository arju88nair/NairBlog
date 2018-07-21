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

- Index.php 
loads the Composer generated autoloader definition, and then retrieves an instance of the Laravel application from bootstrap/app.php script. 
- HTTP / Console Kernels
Next, the incoming request is sent to either the HTTP kernel or the console kernel, depending on the type of request that is entering the application. These two kernels serve as the central location that all requests flow through.
The HTTP kernel extends the Illuminate\Foundation\Http\Kernel class, which defines an array of bootstrappers that will be run before the request is executed. 
Have middlewares
The method signature for the HTTP kernel's handle method is quite simple: receive a  Request and return a Response. Think of the Kernel as being a big black box that represents your entire application. Feed it HTTP requests and it will return HTTP responses.
- Service Providers
 Kernel bootstrapping actions is loading the service providers for your application. All of the service providers for the application are configured in the  config/app.php configuration file's providers array. First, the register method will be called on all providers, then, once all providers have been registered, the boot method will be called.
 -Service providers are responsible for bootstrapping all of the framework's various components, such as the database, queue, validation, and routing components
 - Dispatch Request
Once the application has been bootstrapped and all service providers have been registered, the  Request will be handed off to the router for dispatching. 


> index.php -> bootstrap/app.php(instance from autoload of composer) -> HTTP/Console kernel -> Check the bootrappers -> Request handler

-------

- Service container is a powerful tool for managing class dependencies and performing dependency injection. Dependency injection is a fancy phrase that essentially means this: class dependencies are "injected" into the class via the constructor or, in some cases, "setter" methods.


- Facades 
provide a "static" interface to classes that are available in the application's service container. 

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