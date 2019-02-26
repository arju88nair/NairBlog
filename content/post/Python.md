---
title: "Python"
date: 2019-01-07T12:01:26+05:30
tags: ['Python']
draft: false
---

## Lists

Collection of elements

[0, 1, 2, 3, 4, 5]

---

##  List Comprehension
Allow you to create lists with a for loop with less code.


```

>>> my_list = []
>>> for x in range(10):
...     my_list.append(x * 2)
... 
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

// LC

>>> comp_list = [x * 2 for x in range(10)] 
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]


---
comp_list = [x ** 2 for x in range(7) if x % 2 == 0]

```

Combining two lists

```
>>> nums = [1, 2, 3, 4, 5]
>>> letters = ['A', 'B', 'C', 'D', 'E']
>>> nums_letters = [[n, l] for n in nums for l in letters]
#the comprehensions list combines two simple lists in a complex list of lists.
>>> print(nums_letters)
>>> print(nums_letters)
[[1, 'A'], [1, 'B'], [1, 'C'], [1, 'D'], [1, 'E'], [2, 'A'], [2, 'B'], [2, 'C'], [2, 'D'], [2, 'E'], [3, 'A'], [3, 'B'], [3, 'C'], [3, 'D'], [3, 'E'], [4, 'A'], [4, 'B'], [4, 'C'], [4, 'D'], [4, 'E'], [5, 'A'], [5, 'B'], [5, 'C'], [5, 'D'], [5, 'E']]
>>>

```


## Iterators

Iterable is a “sequence” of data, you can iterate over using a loop.

```
>>> hasattr(str, '__iter__')
True  
>>> hasattr(bool, '__iter__')
False
```

- `iterr()` method is called on the object to converts it to an iterator object.
-  `next()` method is called on the iterator object to get the next element of the sequence.
-  `StopIteration` exception is raised when there are no elements left to call.

## Generators

- Convenient way to use Iterators
- Evaluating the elements on demand
- When you call a normal function with a return statement the function is terminated whenever it encounters a return statement.
- In a function with a yield statement the state of the function is “saved” from the last call and can be picked up the next time you call a generator function.

# Difference between LC and GE

```
>>> list_comp = [x ** 2 for x in range(10) if x % 2 == 0]
>>> gen_exp = (x ** 2 for x in range(10) if x % 2 == 0)
>>> print(list_comp)
[0, 4, 16, 36, 64]
>>> print(gen_exp)
<generator object <genexpr> at 0x7f600131c410>

```

`The generator yields one item at a time — thus it is more memory efficient than a list.`

- List comprehensions are better when you want to iterate over something multiple times
-  If you want to store and use the generated results -> LC

- A List Comprehension, just like the plain range function, executes immediately and returns a list.

- A Generator Expression, just like xrange returns and object that can be iterated over.

----

## Virtual environments
Isolated Python environments for Python libraries

- `virtualenv` - 
It works by installing a bunch of files in a directory (eg: env/), and then modifying the PATH environment variable to prefix it with a custom bin directory (eg: env/bin/). An exact copy of the python or python3 binary is placed in this directory, but Python is programmed to look for libraries relative to its path first, in the environment directory. 
`pyenv` and many others

---

## Env

```
sudo apt install python3-pip
sudo apt install python3-venv
python3.6 -m venv my_env
source my_env/bin/activate
```

---
## Reversing
```
>>> a = '1232'
>>> a[::-1]
'2321'```