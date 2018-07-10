---
title: "Tidbits"
date: 2018-07-10T21:36:16+05:30
---

## Make command

 - The make command accepts targets as command line arguments. These targets are usually specified in a file named 'Makefile', which also contains the associated action corresponding to the targets.
 
 ***


 ## Splat operator
 
 This feature allows you to capture a variable number of arguments to a function, combined with "normal" arguments passed in if you like. It's easiest to see with an example:

 ```   function concatenate($transform, ...$strings) {
        $string = '';
        foreach($strings as $piece) {
            $string .= $piece;
        }
        return($transform($string));
    }

    echo concatenate("strtoupper", "I'd ", "like ",
        4 + 2, " apples");
        ```
