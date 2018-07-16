---
title: "PHP 2"
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