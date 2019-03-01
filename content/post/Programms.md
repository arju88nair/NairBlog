---
title: "Programms"
date: 2018-07-22T13:51:09+05:30
tags : [
    "Programms",
    "Interview",
   ]
---

## Factorial

```
<?php

 $number = 6;                   /*number to get factorial */
 $fact   = 1;
 for($k=1;$k<=$number;++$k)    
       {
          $fact =  $fact*$k;
       }
 echo "Factorial of $number is ".$fact;
 
 
?> 
```
---

## Factorial (Recursion)

```

function factorial($number) {          
        if ($number < 2) { 
            return 1; 
        } else { 
            return ($number * factorial($number-1)); 
        } 
    }

```

## Fibonacci

```
a, b = 1, 1
total = 0
while a <= 10:
    a, b = b, a+b  # the real formula for Fibonacci sequence
    print(a)


```

## Amstrong

```
<?php
 
        
        $number = $_POST[ 'number' ];      // get the number entered by user
       
        $temp = $number;
        $sum  = 0;
       
        while($temp != 0 )
        {
            $remainder   = $temp % 10; //find reminder
            $sum         = $sum + ( $remainder * $remainder * $remainder ); 
            $temp        = $temp / 10; 
 
       }
        if( $number == $sum )
        {
            echo "$number is an Armstrong Number";
        }else
        {
            echo "$number is not an Armstrong Number";
        }
    
```
---

## Reverse of any number

```
 $rev=0;
         $num=$_POST['rev'];
           

          while($num>=1)
                {
                  $re=$num%10;
                  $rev=$rev*10+$re;
                  $num=$num/10;
                 }

```
---

## Prime or not

```
function primeCheck($number){
    if ($number == 1)
    return 0;
    for ($i = 2; $i <= $number/2; $i++){
        if ($number % $i == 0)
            return 0;
    }
    return 1;
}

```
---

## Prime to n

```

function primeno($n){

  for($i=1;$i<=$n;$i++){  //numbers to be checked as prime

          $counter = 0; 
          for($j=1;$j<=$i;$j++){ //all divisible factors


                if($i % $j==0){ 

                      $counter++;
                }
          }

        //prime requires 2 rules ( divisible by 1 and divisible by itself)
        if($counter==2){

               print $i." is Prime <br/>";
        }
    }
} 

primeno(100);       

```
---


## Inverted star diagram

```
for($i=$rows;$i>=1;--$i)
     {
         for($space=0;$space<$rows-$i;++$space)
            echo "  ";
         for($j=$i;$j<=2*$i-1;++$j)
           echo "* ";
         for($j=0;$j<$i-1;++$j)
             echo "* ";
         echo "<br />";
     }

```
---

## * Isocless

```
 for($i=1;$i<=$rows;$i++)
        {
 
           for($j=1;$j<=$i;$j++)
              {
                echo "*";
              }
            echo "<br />";
        
        }
        
```

---
## Largest product of palindrome

```
// The largest palindrome made from the product of two 3-digit numbers.
 
import math
def isPal(x):
    x=str(x)
    t=x[::-1]
    if(x==t):
        return True
    else:
        return False
max=0
for i in range(999,99,-1):
    for j in range(999,99,-1):
        if(isPal(i*j)):
            if((i*j)>max):
                max=(i*j)
print(max)

```

## Occurrence of sub-string

>`match()` method searches a string for a match against a regular expression, and returns the matches, as an Array object. 
```
var temp = "This is a string.";
var count = (temp.match(/is/g) || []).length;
console.log(temp.match(/is/g) || []);
```

--- 

##  Reversel of string

```
$res=0;

while ($x <0)
{
    $res=($res*10)+($x%10);
    $x/-10;
    
}



Also return str_x[:half_num] == str_x[::-1][:half_num]
```