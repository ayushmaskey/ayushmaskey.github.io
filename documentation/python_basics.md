# Python

* [John DeNero UC Berkley 61a](https://cs61a.org/)
* [61a book](http://composingPrograms.com)
* [python tutor](http://pythontutor.com/composingprograms.html#mode=edit)
* [Al Sweigart -automate boring stuff](https://automatetheboringstuff.com/)


higher order function: fxn as parameter, return fxn, fxn inside fxn, lambda
test driven development: python3 -m doctest file.py 
troubleshooting: @trace decorator
data abstraction

## Table of Content
 * [run python](#run-python)
 * [make executable](#make-executable)
 * [Basic math](#basic-math)
 * [Operators](#operators)
 * [Data types](#data-types)
 * [Data type conversion](#data-type-conversion)
 * [condition](#condition)
 * [assert](#assert)
 * [loop](#loop)
 * [try-except](#try-except)
 * [Sequences](#sequences)
   * [Array](#array)
   * [List basic](#list-basic)
     * [List method](#list-method)
   * [String basic](#string-basic)
     * [String methods](#string-methods)
   * [Tuples](#tuples)
   * [Dictionary](#dictionary)
     * [Dictionary method](#dictionary-method)
 * [Regular expression](#regular-expression)
 * [pyperclip](#pyperclip)
 * [reading and writing files](#reading-and-writing-files)
 * [functions](#functions)
   * [built in function](#built-in-function)
   * [import library](#import-library)
   * [user defined function](#user-defined-function)
   * [higher order function](#higher-order-function)
   * [return statement](#return-statement)
   * [self reference](#self-reference)
   * [why higher order](#why-higher-order)
   * [lambda](#lambda)
   * [def vs lambda](#def-vs-lambda)
   * [recursion](#recursion)
   * [function currying](#function-currying)
   * [functional abstraction](#functional-abstraction)
 * [mutual recursion](#mutual-recursion)
 * [test driven development](#test-driven-development)


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

for i in range(4) 		# 0 inclusive and 4 exclusive  && i+=1 --> i = 0,1,2,3

for i in range(1,10,2) 		# 1 inclusive && 10 exclusive && i+=2 --> i = 1,3,5,7,9

for i in range(5,-2,-1) 	# 5 inclusive && -2 exclusive && i-=1 --> i = 5,4,3,2,1,0,-1

break 
continue
```

## try-except
```python
try:
  return 42/x
except ZeroDivisionError:			#if x == 0
  print('Bad Input')
```

## Sequences 
 * ordered sequence
 * list, tuple, string, array

## [Array](https://docs.python.org/3/library/array.html)
looks useless
```python
from array import array
x= array([2,4,6,4]) 				#array useful when doing arithmetic with inside elements
x/2 = (1,2,3,2)
```

## [List basic](https://docs.python.org/3/tutorial/introduction.html#lists)
```python
>>>myList = [[6,5,2],['rat','cat','hat'],'hello']
>>>myList[0]
[6,5,2] 
>>>myList[1][2]
'hat'
>>>myList[-1]
'hello'
>>>myList[-2][-3]
'rat'
>>>myList[1][0:2]				# 2 excluded
['rat','cat']
>>>myList[1][:] 				# start at 0 inclusive, end at last inclusive
['rat','cat','hat']
>>>myList[1][:2]				# 0 to 1
['rat','cat'] 
>>>len(myList[1])
3
>>>myList[1][1]
'kitty'
>>>del myList[2]
>>>'dog' in myList[1] 
False
>>>'dog' not in myList[1]
True

#mutable data type like list and dictionary are stored as references/pointers
>>>import copy
>>>copy.copy(myList) 				# make copy of mutable data
>>>copy.deepcopy(myList)			# make copy of list and the inner lists

>>>[1,2,3] + ['a','b','c']
[1,2,3,'a','b','c'] 
>>>[1,2,3] * 3
[1,2,3,1,2,3,1,2,3]

>>>for i in range(len(someList))

# swap values without temp variable
>>>a,b=1,2
>>>a,b=b,a
```
## [List method](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
```python
>>>cat = ['fat', 'orange', 'kitty']
>>>size, color, name = cat
>>>cat.index('fat')
0
>>>cat.append('lazy')
>>>cat
['fat', 'orange', 'kitty', 'lazy']
>>>cat.insert(1, 'female')
>>>cat
['fat', 'female', 'orange', 'kitty', 'lazy']
>>>cat.remove('kitty')
>>>cat
['fat', 'female', 'orange', 'lazy']
>>>cat.sort()
>>> cat
['fat', 'female', 'lazy', 'orange']
>>>cat.sort(reverse=True)
>>> cat
['orange', 'lazy', 'female', 'fat']
>>>cat.sort(key=str.lower) 			# sorting done by ASCII uppercase before lower
>>> cat
['fat', 'female', 'lazy', 'orange']
```

## [String basic](https://docs.python.org/3.1/library/string.html)
similar to list
big difference: string is immutable ie cannot be changed
```python
>>>myString = 'that is a cat named puppy'
change = ['cat','dog']
>>>myString = myString[0:myString.index(change[0])] + \
	change[1] + myString[myString.index(change[0]) + \
	len(change[0]):] 
>>>myString
'that is a dog named puppy'

# escape " ` " using backslash
\'

#not valid in string coz immutable
del myString[5]
myString.append('.')
```

## [String methods](#https://docs.python.org/3.1/library/stdtypes.html#string-methods)
```python
#title case
str.upper(), str.lower(), str.isupper(), str.islower(), str.istitle()

str.isalpha(), str.isalnum(), str.isdecimal(), str.isspace()

# beginning and ending of string
str.startswith(), str.endswith()

#join and split
>>>':'.join('a','b','c')
a:b:c
>>>'a:b:c'.split(':')
('a','b','c')

#pad left, right or center with spaces or string to make right length
>>>'Hello'.rjust(10)
'     Hello'
>>>'Hello'.ljust(6,'*')
'Hello*'
>>>'Hello'.center(15,'-')
'-----Hello-----'

# remove white space
str.strip(). str.rstrip(), str.lstrip()

# removes all possible combination of ampS from start and end
>>>'SpamSpamBaconSpamEggsSpamSpam'.strip('ampS' or 'mapS' or 'pSam')
'BaconSpamEggs'
```

## [Tuples](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences)
```python
similar to list but uses () instead of []
tuples are immutable like string
```

## [Dictionary](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)
```python
>>>cat = {'name': 'kitty', 'size': 'fat', 'color': 'orange', 12: 'age'}
>>>cat['name']
'kitty'

#Unordered
>>>cat = {'name': 'kitty', 'size': 'fat', 'color': 'orange', 12: 'age'}
>>>dog = {12: 'age','name': 'kitty', 'size': 'fat', 'color': 'orange'}
>>>cat == dog
True
```

## Dictionary method
```python
keys(), values(), items()

# just values
for i in cat.values():
	print(i)

# just keys
for i in cat.keys():
	print(i)

for i in cat.items():
	print(i)

# keys and values
for k,v in cat.items():
	print('Key: ' + k + ' Value: ' + v)

>>>'name' in cat.keys()
True
>>>'fat' not in cat.values()
False

# returns 0 if there is no key called length
>>>cat.get('length',0)
0

if 'length' not in cat:	
	cat['length'] = '12 inch' 
# or cat.setdefault('length', '12 inch')
```

## [Regular expression](https://docs.python.org/3/howto/regex.html)
```python
>>>import re
>>>strBlob = '555-555-5555'
# create regex object and use r to search as raw data
>>>strPattern = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')

# pass the string to search into regex object's search method
>>>matchedObjects = strPattern.search(strBlob)

# call group to return the first instance of matched expression
>>>print(matchedObjects.group())
555-555-5555

#parethesis in regular expression

# search for regex either bracket or complete
>>>strPattern = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)')
>>>strBlob = '(555) 555-5555'
>>>matchedObjects = strPattern.search(strBlob)	
>>>areaCode, mainNumber = matchedObjects.groups()

>>>matchedObjects.group(0)
'555-555-5555'
>>>areCode = matchedObjects.group(1)
>>>matchedObjects.group(2)

#matching multipe groups with |

# finds first instace of batman or wonder woman
>>>regHero = re.compile(r'batman|wonder woman')
>>>mo1 = regHero.search('batman, superman, wonder woman')	
>>>mo2 = regHero.search('superman, wonder woman, batman')
>>>mo1.group()
batman
>>>mo2.group()
wonder woman

>>>regBat = re.compile(r'bat(man|mobile|cave|girl)')
# finds batman and batwoman. pattern in (wo)? is optional
>>>regBat = re.compile(r'bat(wo)?man')
# finds batman, batwoman, batwowoman, batwowowoman etc
>>>regbat = re.compile(r'bat(wo)*man')
# atleast 1 - finds batwoman, batwowoman but not batman
>>>regbat = re.compile(r'bat(wo)+man')

(Ha){3}  -->HaHaHa
(Ha){3,5}--> HaHaHa, HaHaHaHa, HaHaHaHaHa
(Ha){3, }--> Unbounded - 3 or more
(Ha){ ,5}--> Unbounded - 0 to 5

# searching for parethesis need escape charater even in raw string
/(, /), /|, /*, /+

#Python regex are greedy by default - ie finds the longest possible string
# finds the longest possible
>>>greedyRegex = re.compile(r'(Ha){3,5}')
# find the shortest possible
>>>nonGreedyRegex = re.compile(r'(Ha){3,5}?')
>>>mo1 = greedyRegex.search('HaHaHaHa')
>>>mo2 = nonGreedyRegex.search('HaHaHaHa')
>>>print(mo1.group() )
HaHaHaHa
>>>print(mo2.group() )
HaHaHa

>>>phoneRegex1 = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
>>>phoneRegex2 =  re.compile(r'(\d\d\d)-(\d\d\d)-(\d\d\d\d)')
#finds all the matching exp in the string
>>>phoneRegex1.findall('asdf ads 898-959-5265 afw da 595-898-8747')
['898-959-5265', '595-898-8747'] 
#list of tuples
>>>phoneRegex2.findall('asdf ads 898-959-5265 afw da 595-898-8747')
[('898', '959', '5265'), ('595', '898', '8747')] 


\d - digits 0 to 9
\D - not (digits 0 to 9)
\w - digits, letters, and underscore
\W - not (digits, letters, and underscore)
\s - space, tab, newline
\S - not (space, tab, newline)
[0-5] - matches 0,1,2,3,4,5


# any number of digits followed by a whitespace and then any number of words
xReg = re.compile(r'\d+\s\w+')

# find vowels from string
userDef1 = re.compile(r'[aeiuoAEIOU]')

# all lower and upper alpha + digits
userDef2 = re.compile(r'[a-zA-Z0-9]')

# all lower and ending in period. no need \. inside []
userDef3 = re.compile(r'['[a-z.]')

# caret inside [] finds non regex from string
userDef4 = re.compile(r'[^aeiuoAEIOU]')

# caret as raw string means must start with given expression
userDef5 = re.compile(r'^[a-e]+')

# dollar sign means ends with given expression
userDef6 = re.compile(r'[a-e]+$')

# whole string is digits
userDef7 = re.compile(r'^d+$')

# one wild character with dot. everything but newline
userDef8 = re.compile(r'.at')

# more than one wild character with .*
r'.*'
# greedy wild character with .*?
r'.*?'

# case insensitive
re.compile(r'ayush',re.IGNORECASE)

#String substitution with regex
>>>xReg = re.compile(r'Ayush \w+')
>>>xReg.sub('King', 'My name is Ayush Maskey')
My name is King
>>>censorAgents = re.compile(r'Agent (/w) w+')
>>>censorAgents.sub('\1***', 'Agent James and Agent Bond went undercover')
Agent J*** and Agent B*** went undercover


# complicated regex into readable
# re.VERBOSE ignores white space and comments
# expression inside ''' triple quote - triple quote extends to multiple lines

phoneRegex = re.compile(r'((\d{3}|\(\d{3}\))?(\s|-|\.)?\d{3}(\s|-|\.)\d{4}(\s*(ext|x|ext.)\s*\d{2,5})?)')

VS

phoneRegex = re.compile(r'''(]
    (\d{3}|\(\d{3}\))?            # area code
    (\s|-|\.)?                    # separator
    \d{3}                         # first 3 digits
    (\s|-|\.)                     # separator
    \d{4}                         # last 4 digits
    (\s*(ext|x|ext.)\s*\d{2,5})?  # extension
    )''', re.VERBOSE)
```

## [pyperclip](https://pypi.python.org/pypi/pyperclip)
```python
# paste anything in clipboard
pyperclip.copy('Hello')
pyperclip.paste()
```

## reading and writing files
```python
>>>import os
# ubuntu - home/amaskey/Google 
# Windows - home\\amaskey\\Google 
>>>folder = os.path.join('home','amaskey','Google')
>>>folder
'home/amaskey/Google'
>>>files = ['file1.txt','file2.txtx','file3.txt']
>>>for fileName in files:
	os.path.join(filePath, fileName)
>>>os.getcwd()
PWD

>>>open('filename')
>>>s = set( open('~/Document.../filename').read().split() )
>>>{w for w in s if s == s[::-1] and len(s) > 3}
>>>{w for w in s if s[::-1] in s and len(s) == 5}
```

## Functions
 * Domain --> set of all possible inputs
 * Range --> set of all possible outputs
 * give each function exactly one job --> sissor not swiss army knife
 * dont repeat yourself (DRY) --> implement process once but execute many times
 * define function generally --> one general way to plug into scoket instead for 2 ppin, 2 pin etc etc


## built in function
```python
len()
print( str1 + str2 + str(3) ) 
print(str1, str2)
print("ayush", end='') 		# end of print  is usally \n but here it is replaced by ''
print(str1, str2, sep=',') 	# usually separated by str1 str2 but here str1,str2 
input() 			# waits for user input as string
```

## Import library
```python
from random import * 
randint(1,9) 					# 1 and 9 inclusive

from random import randint 			# use randint()

import random 					# use random.randint()

import sys 
sys.exit()					# exit the program
```

## user defined function
```python
def fnName(parameter):
	operations
	return x

def fnName(p1, p2=100)
	operations
	return x,y

""" return more than one variable
p2=100 as default if it is not defined when calling the fxn"""

```
### function generalization

###### generalizing with constant

> simplest form
```python
from math import pi, sqrt

def area_square(r):
  return r * r

def area_circle(r):
  return r * r * pi

def area_hexagon(r):
  return r * r * sqrt(3) / 2

#problem --> calculates area of negative length
```

> simple fix
```python
from math import pi, sqrt

def area_square(r):
  assert r > 0, 'A length must be positive'
  return r * r

def area_circle(r):
  assert r > 0, 'A length must be positive'
  return r * r * pi

def area_hexagon(r):
  assert r > 0, 'A length must be positive'
  return r * r * sqrt(3) / 2

#problem --> violating DRY preinciple
```

> factor out common
```python
from math import pi, sqrt

def area(r, shape_constant)
  assert r > 0, 'A length must be positive'
  return r * r * shape_constant

def area_square(r):
  return area(r, 1)

def area_circle(r):
  return area(r, pi)

def area_hexagon(r):
  return area(r, 3 * sqrt(3) / 2 )

# generalized with constant
```

###### generalizing over computational process

> simplest form
```python

def sum_naturals(n):
  """sum of first N natural numbers
  >>> sum_naturals(5)
  15
  """
  total, k = 0, 1
  while k <= n:
    total, k = total + k, k + 1
  return total

def sum_cubes(n):
  """sum of first N cubes natural numbers
  >>> sum_cubes(5)
  225
  """
  total, k = 0, 1
  while k <= n:
    total, k = total + pow(k, 3), k + 1
  return total 

# problem --> violates DRY principle
```

> higher order example 1
> function as parameter
```python

def identity(k):
  return k

def cube(k):
  return pow(k, 3)

def summation(n, term):
  """sum of the first N terms of a sequence"""
  >>> summation(5, cube)
  225
  """
  total, k = 0, 1
  while k <= n:
    total, k = total + term(k), k + 1
  return total

def sum_naturals(n):
  """sum of first N natural numbers
  >>> sum_naturals(5)
  15
  """
  return summation(n, identity)

def sum_cubes(n):
  """sum of first N cubes natural numbers
  >>> sum_cubes(5)
  225
  """
  return summation(n, cube) 

def pi_terms(n)
  return 8 / mul(4 * k - 3, 4 * k - 1)

>>>summation(1000000, pi_term)
3.141592...

#higher order function
```


## [higher order function](http://composingprograms.com/pages/16-higher-order-functions.html) 

 * [function as parameter](#function-as-parameter)

> higher order example 2
> function that returns function
> function inside function
> nested def
```python
def make_adder(n):
  """ return a function that takes one argument K and return K + N.
  >>> add_three = make_adder(3)
  >>> add_three(4)
  7
  """
  def adder(k):
    return k + n
  return adder

>>> maker_adder(1) (2)
3
>>> add_one = make_adder(1)
>>> add_one(2)
3 

```

* nested def statement
* function as return value
* when adder it is returned after the function is built, it is not accessive in global frame
* now add_one points to adder(k) so make_adder frame is still active
* add_one lives in global but its parent is make_adder
* when add_one(2) is called new frame is created
* parent of this third frame has parent of make_adder (not global)
* every user defined function has a parent frame which is often global
* but if there is nested def statement, inner def's parent will be outer def
* parent of a function is a frame in which it was defined


> nest def make_adder simplified into two def
```python
>>> def f(x, y):
...   return g(x)
>>> def g(a):
... return a + y
>>> f(1,2)
3
```
> error coz y is not defined in g(a)
> need to call g(a,y)
> environment is sequence of frames
> parent of function f and g is global 

* functions are first class: fxn can be manipulated as values in our programming language
* higher-order function: 
  1. a function that takes a function as an agument value 
  2. returns a function as a return value
  3. or both

* use of higher-order
  * express general methods of computation
  * remove repetition from programs
  * separate concerns among functions

> higher order example 3
> call same function twice

```python
def apply_twice(f, x):
  return f(f(x))

def square(x):
  return x * x

>>> square(10)
100
>>> apply_twice(square, 3)
81

# f is called twice
# creates two frame, one for each f
# inner f called first and then the result is passed to outer f
```

> higher order example 1
> function as parameter in a loop
```python
def repeat(f, x):
  while f(x) != x:
    x = f(x)
  return x

def g(y):
  return (y + 5) // 3

>>> repeat(g, 5)
2

# loop 1 --> f = g, x = 5 --> f(x) or g(y) = 5 + 5 // 3 = 3 --> 3 != 5 --> x = 3
# loop 2 --> f(x) = 3 + 5 // 3 = 2 --> 2 != 3 --> x = 2
# loop 3 --> f(x) = 2 + 5 // 3 = 2 --> 2 == 2 --> exit loop
# return 2 
```

> higher order example 3

```python
def make_adder(n):
  def adder(k):
    return k + n
  return adder

def square(x): 
  return x * x

def triple(x):
  return 3 * x

def compose1(f,g):
  def h(x):
    return f(g(x))
  return h

>>> fxn1 = compose1(square, triple)
>>> fxn1(5)
225

# triple of 5 is 15
# square of 15 is 225
# g is called first so triple first
 
>>> fxn2 = compose1(triple, square)
>>> fxn2(5)
75

# square(5) = 25 
# triple(25) = 75

>>> fxn3 = compose1(square, make_adder(2) )
>>> fnx3(3)
25

# maker_adder(2) function that adds two to input
# make_adder(2)(3) = 5
# square(5) = 25

>>> fxn3 = compose1(square, make_adder(2) )(3)
25
;
```

## return statement
 * completes the evaluation of a call expression and provides its value
 * for  user defined function f(x), execute f's body in a new environment
 * return statement goes back to previous environment with a value for f(x)
 * only one return statement is ever executed

```python
def search(f):
	"""start and 0 and work its way up until it finds a true value
	"""
	x = 0
	while True:
		if f(x):
			return x
		x += 1

def is_three(x):
	return x == 3

def square(x):
	return x * x

def positive(x):
	return max(0, square(x) - 100)

>>>positive(1)
0
>>>positive(10)
0
>>>positive(11)
21
>>>search(positive)
11

# search(postive) give smallest x that gives positive value


def inverse(f):
	"""return g(y) such that g(f(x)) --> x"""
	return lambda y: search(lambda x: f(x) == y)

>>> sqrt = inverse(square)
>>> sqrt(256)
16

# only works for perfect square root

def inverse1(f):
	def aux_for_y(y):
		def aux_for_x(x):
			return f(x) == y
		return search(aux_for_x)
	return aux_for_y

# simplifying inverse with inverse1
```

## self reference
```python
def print_all(x):
	print(x)
	return print_all

>>> print_all(4)
4
<function print_all at 0x7fdaf755a1e0>
>>> print_all(4)(5)
4
5
<function print_all at 0x7fdaf755a1e0>
# can call print_all with as many parameter coz return is always bound to print_all
```

```python
def print_sum(x):
	print(x)
	def next_sum(y):
		return print_sum(x+y)
	return next_sum

>>> print_sum(1)(3)(5)
1
4
9
<function print_sum.<locals>.next_sum at 0x7f6dbd436f28>

```
* first call to goes to print_sum but subsequent call goes to next_sum coz next_sum is returned which is bound to print_sum(1) with parameter (3)
* second call goes straight to next_sum(3) with x as 1 which add a and y and calls print_sum, add return next_sum again
* in the final call, next_sum is called with x = 4, coz that is the value in parent environment and y as 5 --> print_sum(1)(3)(5) reduces to next_sum(5) with x=4 from parent
* sum is being memorized along the way
* new sum is passed as argument x for print_sum and the next one is y

## why higher order

> play 2 secs of mario intro
```python
from wave import open
from struct import Struct
from math import floor

frame_rate = 11025

def encode(x):
	"""Encode float x between -1 and 1 as two bytes
	https://docs.python.org/3/library/struct.html)
	"""
	i = int(16284 * x)
	return Struct('h').pack(i)

def play(sampler, name="song.wav", seconds=2):
	"""Write the output of a sampler function as a wav file
	https://docs.python.org/3/library/wave.html
	"""
	out = open(name, 'wb')
	out.setnchannels(1)
	out.setsampwidth(2)
	out.setframerate(frame_rate)
	t = 0
	while t < seconds * frame_rate:
		sample = sampler(t)
		out.writeframes(encode(sample))
		t = t + 1
	out.close()

def tri(frequency, amplitude = 0.3):
	"""A continuous triange wave"""
	period = frame_rate // frequency
	def sampler(t):
		saw_wave = t / period - floor(t / period + 0.5)
		tri_wave = 2 * abs(2 * saw_wave) - 1
		return amplitude * tri_wave
	return sampler

c_freq, e_freq, g_freq = 261.63, 329.63, 392.00

def both(f, g):
	return lambda t: f(t) + g(t)

def note(f, start, end, fade=0.01):
	def sampler(t):
		seconds = t / frame_rate
		if seconds < start:
			return 0
		elif seconds > end:
			return 0
		elif seconds < start + fade:
			return (seconds -start) / fade * f(t)
		elif seconds > end - fade:
			return (end - seconds) / fade * f(t) 
		else:
			return f(t)
	return sampler

def mario_at(octave):
	c, e = tri(octave * c_freq), tri(octave * e_freq)
	g, low_g = tri(octave * g_freq), tri(octave * g_freq / 2)
	return mario(c, e, g, low_g)

def mario(c, e, g, low_g):
	z = 0
	song = note(e, z, z + 1/8)
	z += 1/8
	song = both(song, note(e, z, z + 1/8))
	z += 1/4
	song = both(song, note(c, z, z + 1/8))
	z += 1/4
	song = both(song, note(e, z, z + 1/8))
	z += 1/8
	song = both(song, note(g, z, z + 1/4))
	z += 1/4
	song = both(song, note(low_g, z, z + 1/4))
	z += 1/2
	return song

play(both(mario_at(1), mario_at(1/2)) )
```

## [lambda](https://docs.python.org/3/howto/functional.html#small-functions-and-the-lambda-expression)

* a function with formal parameter x that returns the value
* no need return keyword
* only single expression
* therefore only simple functions
* cannot contain statements
* not common in python but some language use it extensively

```python
>>>f = lambda x: x+5
>>>f
<function>
>>>f()
TypeError: <lambda>() missing 1 required positional argument: 'x'
>>> f(3)
8
>>>avg = lambda x,y,z: (x+y+z) / 3
>>>avg(2,3,4)
3.0

#different lambda
>>> f = lambda : 5
>>> g = lambda : 5
>>> f == g
False
>>> f
<function <lambda> at 0x7fc22528ebf8>
>>> g
<function <lambda> at 0x7fc22528eb70>


#pointing to same lambda
>>> f = lambda : 5
>>> g = f
>>> g
<function <lambda> at 0x7fc22528ebf8>
>>> f
<function <lambda> at 0x7fc22528ebf8>

# lambda called twice??
>>> def foo(x): 
...     return x() 
... 
>>> goo = foo(lambda: 5)

```
## def vs lambda
* both create function with same domain, range and behavior.
* both functions have as their parent the frame in which they are defined
* def creates a function and binds it to var 
* def create function and bind to variable at the same time
* lambda creates function without binding to var
* lambda can be bound to var but needs to be assigned
* def --> can have local var, call other function, loops etc
* lambda --> only parameter and return
* all lambda can be rewritten as def
* only def statement gives the function an intrinsic name 
* makes difference in environment diagram

```python
>>> def f():
...
>>> f
<function f at ...>
>>> square = lambda x: x * x
>>> square
<function <lambda> at ...>
````
## recursion

## function currying


## functional abstraction
```python
- need to know number of argument
- dont care about intrinsic name of function - name can be assigned to anything else. helps other humans and myself read the program
- need to know what fuction does/returns/prints
- dont care how it computes 
```

### mutual recursion 

luhn sum- credit card number 

## test driven development
```python
- write test before writing a function

from ucb import trace	# create my own trace for testing 

@trace  	#trace decorator function is doing instead of prints everywhere
def gcd(n,m):
  """
  >>> gcd(12,8)
  4
  >>>find all possible cases
  """
  now implement the function
```






