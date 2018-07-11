+++
title = "Tidbits"
description = "Some tidbits I came across"
tags = [
    "random",
    "linux",
   ]
date = "2014-04-02"
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
