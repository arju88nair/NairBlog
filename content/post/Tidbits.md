+++
title = "Tidbits"
description = "Some tidbits I came across"
tags = [
    "random",
    "linux",
   ]
date = "2018-07-11"
categories = [
    "Learning",
]
+++

## Make command

 > The make command accepts targets as command line arguments. These targets are usually specified in a file named 'Makefile', which also contains the associated action corresponding to the targets.
 
 
 ***





## Splat operator
 
 This feature allows you to capture a variable number of arguments to a function, combined with "normal" arguments passed in if you like. It's easiest to see with an example:

 ``` 
   
   function concatenate($transform, ...$strings) {
        $string = '';
        foreach($strings as $piece) {
            $string .= $piece;
        }
        return($transform($string));
    }
    
    echo concatenate("strtoupper", "I'd ", "like ",
        4 + 2, " apples");
 ```
 
 ## SVN CPIO command
 > To get the different file changes between two revisions, remove the first empty characters and create folder structure and paste i
 
 ```
 sudo svn diff -r 8:HEAD --summarize | cut -c9-99999 | cpio -pvdmu /var/www/html/Blah
```

## BASH while loop
```


#!/bin/bash
# This script opens 4 terminal windows.

i="0"

while [ $i -lt 4 ]
do
xterm &
i=$[$i+1]
done


```

## Code checking
-  Make sure that the code got enough comments and documentation
- Make sure that there aren't unwanted variables and which can be turned to globals
- Function static or non-static

## CSS background shadow for user images

`box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.5)`


----

 The use of floated elements for layout is getting more and more discouraged with the use of better alternatives.

`display: inline-block - Better`
`Flexbox` - Best (but limited browser support

`Clearfix`- Automatically [clear](https://i.stack.imgur.com/gYRqS.jpg) its child elements

---

## Domain Name

- The `A record` maps a name to one or more IP addresses, when the IP are known and stable.

- The `CNAME` record maps a name to another name. It should only be used when there are no other records on that name.

- The `ALIAS` record maps a name to another name, but in turns it can coexist with other records on that name.

- The `URL record` redirects the name to the target name using the HTTP 301 status code.

Rules

- The A, CNAME, ALIAS records causes a name to resolve to an IP. Vice-versa, the URL record redirects the name to a destination. 

- The URL record is simple and effective way to apply a redirect for a name to another name, for example to redirect www.example.com to example.com.
- The A name must resolve to an IP, the CNAME and ALIAS record must point to a name.


What to use?

- Use an A record if you manage what IP addresses are assigned to a particular machine or if the IP are fixed (this is the most common case)

- Use a CNAME record if you want to alias a name to another name, and you don’t need other records (such as MX records for emails) for the same name

- Use an ALIAS record if you are trying to alias the root domain (apex zone) or if you need other records for the same name

- Use the URL record if you want the name to redirect (change address) instead of resolving to a destination.

---

# PHP fpm
Running your application using a combination of a nginx web-server and a php-fpm server.

 Nginx serves the static files and forwards specific requests to php-fpm while php-fpm executes the PHP code. 

 When a request comes through, php-fpm initiates a PHP child process and the request details are provided as part of the process state (_GET, _POST, and _SERVER, etc). 
 
 The state can’t change during the execution of the PHP script so the only way to get a new set of input data is to destroy the process and start over again.

 ---

 ## Sybil Attach

 > The Sybil attack in computer security is an attack wherein a reputation system(rating system) is subverted by forging identities in peer-to-peer networks
 
 ---


## Memoization
Is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again


