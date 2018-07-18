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