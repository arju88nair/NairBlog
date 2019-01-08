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
<?PHP 

   $first = 0;
   $second = 1;
   echo $first.'&nbsp;,';
   echo $second.'&nbsp;,';
  

  for($limit=0;$limit<10;$limit++)
   {
     $third = $first+$second;
     echo $third.'&nbsp;,';;
     $first = $second;
     $second = $third;
    
   }

?>
```
---


## Fibonacci sum

```
a, b = 1, 1
total = 0
while a <= 4000000:
    if a % 2 == 0:
        total += a
    a, b = b, a+b  # the real formula for Fibonacci sequence
print (total)

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