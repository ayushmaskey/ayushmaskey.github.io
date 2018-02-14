# Python Basics

* [John DeNero UC Berkley 61a](https://cs61a.org/)
* [61a book](http://composingPrograms.com)
* [python tutor](http://pythontutor.com/composingprograms.html#mode=edit)
* [Al Sweigart -automate boring stuff](https://automatetheboringstuff.com/)


higher order function: fxn as parameter, return fxn, fxn inside fxn, lambda
test driven development: python3 -m doctest file.py 
troubleshooting: @trace decorator
data abstraction

## Table of Content
 * [back to ToC](./table_of_content.md)
 * [python basic](./py_basics.md)
   * [run python](#run-python)
   * [make executable](#make-executable)
   * [Basic math](#basic-math)
   * [Operators](#operators)
   * [Data types](#data-types)
   * [Data type conversion](#data-type-conversion)
   * [condition](#condition)
   * [assert](#assert)
   * [loop](#loop)
   * [range](#range)
   * [list comprehension](#list-comprehension)
 * [Sequences - list, dict, string...](./py_sequences.md)
 * [Regular expression](./py_regular_exp.md)
 * [reading and writing files](./py_io.md)
 * [functions](./py_functions.md)
 * [Data Abstraction](./py_data_abstraction.md)
 * [Trees](./py_trees.md)
 * Libraries
   * [pyperclip](./py_lib_pyperclip.md)

ctrl + l --> clear screen

## run python
```bash
#simple run
python3 fileName.py

#run interactively
python3 -i fileName.py

#compile and test run with doctest - no result if no error
python3 -m doctest fileName.py

#run with doctest -show verbose result
python3 -m doctest -v fileName.py

```

## make executable 
ie dont need to type python3 fileName.py
```bash
#ubuntu
chmod +x fileName.py

#windows
.bat file
@py.exe C:\myFolder\filename.py %*
@pause
```

## Basic math
```python
from operator import add, mul, pow, truediv, floordiv, mod
mul(a,b) or a*b
add(a,b) or a+b
pow(a,b) or a**b
truediv(a,b)  or a / b 		# with decimal
floordiv(a,b) or a // b 	# get divident
mod(a,b) or a % b

min(a,b) 
max(a,b)

from math import sqrt
sqrt(16)

'Ayush' * 3 = 'AyushAyushAyush'
```
## Operators
```python
+= (string, int and float)
*= (string, int and float)
-= (int and float)
/= (int and float)
%= (int)

Comparisons: ==, !=, >, <, >= <=
assignment =
Boolean operators - and, or, not
```
## Data types
```python
int, float, string, boolean(True, False), None, list, tuple, array, dictionary
```
## Data type conversion
```python
int(), float(), str()

tuple([ , , ]) 						# convert list to tuple
list(( , , )) 						# convert tuple to list
list('hello') 						# ['h','e','l','l','o'] - convert string to list
```

## condition
```python
if 
elif
else

# and / or short circuiting
>>>True and 1
1
>>>False and 1
False
>>>True or 1
True
>>>False or 1
1
```
## assert

```python
assert 3 > 2, "return string if true"

def area_square(r):
  assert r > 0, "length must be positive"
  return r * r
```

## loop
```python
while():
  #code block goes here

break 
continue

for i in ints:

for s in str:
for <name> in <expression>:
	<suite>
```

```python3
def count(s, value):
	"""count the number of times that value appears in sequence s
	>>> count([1, 2, 1, 2, 1], 1)
	3
	"""
	total = 0 
	for element in s: 
		if element == value:
			total += 1
	return total

>>> count([1, 2, 1, 2, 1], 1)
3

#sequence unpacking in for loop

for x, y in pairs:
	if x == y:
		total = total + 1
```

## range
```python3
for i in range(4) 		# 0 inclusive and 4 exclusive  && i+=1 --> i = 0,1,2,3
for i in range(1,10,2) 		# 1 inclusive && 10 exclusive && i+=2 --> i = 1,3,5,7,9
for i in range(5,-2,-1) 	# 5 inclusive && -2 exclusive && i-=1 --> i = 5,4,3,2,1,0,-1

>>> list( range( -2, 2) )
[-2, -1, 0, 1]
>>> list(range(4))
[0, 1, 2, 3]
>>>

def cheer():
	for _ in range(3):
		print('yes!')
>>> cheer()
yes!
yes!
yes!
>>> 

# '_' means not using that any where 
```
> benefit of range
 * length: ending value - starting value
 * element selection: starting value + index

## list comprehension
```python
>>> odds = [1, 3, 5, 7, 9]
>>> [x+1 for x in odds]
[2, 4, 6, 8, 10]
>>> [x for x in odds if 25 % x == 0]
[1, 5]
>>> [x+1 for x in odds if 25 % x == 0]
[2, 6]
>>> 

def divisor(n):
	return [1] + [x for x in range(2, n) if n % x == 0]
>>> divisor(5)
[1]
>>> divisor(50)
[1, 2, 5, 10, 25]
>>> 

``




