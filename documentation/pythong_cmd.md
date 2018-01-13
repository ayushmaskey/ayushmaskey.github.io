# Python

* [John DeNero UC Berkley 61a](https://cs61a.org/)
* [61a book](http://composingPrograms.com)
* [Al Sweigart -automate boring stuff](https://automatetheboringstuff.com/)


basics: conditional statements,  functions
regular expression (RegEx): pattern matching
higher order function: fxn as parameter, return fxn, fxn inside fxn, lambda
test driven development: python3 -m doctest file.py 
troubleshooting: @trace decorator
data abstraction
external files

## Table of Content
 * [Basic math](#basic-math)
 * [Operators](#operators)
 * [Data types](#data-types)
 * [Data type conversion](#data-type-conversion)
 * [build-in functions](#build-in-function)
 * [loop](#loop)
 * [Import library](#import-library)
 * [try-except](#try-except)
 * [Seqences](#Seqences)
   * [Array](#Array)
   * [List basic](#List-basic)
     * [List method](#List-method)

### Basic math
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
### Operators
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
### Data types
```python
int, float, string, boolean(True, False), None, list, tuple, array, dictionary
```
### Data type conversion
```python
int(), float(), str()
```
### Built-in functions
```
len()
print( str1 + str2 + str(3) ) 
print(str1, str2)
print("ayush", end='') 		# end of print  is usally \n but here it is replaced by ''
print(str1, str2, sep=',') 	# usually separated by str1 str2 but here str1,str2 
input() 			# waits for user input as string
```
### loop
```python
while():
  #code block goes here

for i in range(4) - 0 inclusive and 4 exclusive   && i+=1		#i = 0,1,2,3

for i in range(1,10,2) - 1 inclusive && 10 exclusive && i+=2		#i = 1,3,5,7,9

for i in range(5,-2,-1) - 5 inclusive && -2 exclusive && i-=1		#i = 5,4,3,2,1,0,-1

break 
continue
```

### Import library
```python
from random import * 
randint(1,9) 					# 1 and 9 inclusive

from random import randint 			# use randint()

import random 					# use random.randint()

import sys 
sys.exit()					# exit the program
```

### try-except
```
try:
  return 42/x
except ZeroDivisionError:			#if x == 0
  print('Bad Input')
```

### Seqences 
 * (ordered sequence)
 * list, tuple, string, array

### [Array](https://docs.python.org/3/library/array.html)
looks useless
```
from array import array
x= array([2,4,6,4]) 				#array useful when doing arithmetic with inside elements
x/2 = (1,2,3,2)
```

### [List basic](https://docs.python.org/3/tutorial/introduction.html#lists)
```
myList = [[6,5,2],['rat','cat','hat'],'hello']
myList[0] = [6,5,2] 
myList[1][2] = 'hat'
myList[-1] = 'hello'
myList[-2][-3] = 'rat'
myList[1][0:2] = ['rat','cat'] 			# 2 excluded
myList[1][:] =['rat','cat','hat'] 		# start at 0 inclusive, end at last inclusive
myList[1][:2] = ['rat','cat'] 			# 0 to 1
len(myList[1])
myList[1][1] = 'kitty'				# [[6,5,2],['rat','kitty','hat'],'hello']
del myList[2]  					# [[6,5,2],['rat','kitty','hat']]
'dog' in myList[1] 				# False
'dog' not in myList[1] 				# True

[1,2,3] + ['a','b','c'] = [1,2,3,'a','b','c'] 
[1,2,3] * 3 = [1,2,3,1,2,3,1,2,3]

for i in range(len(someList))

cat = ['fat', 'orange', 'kitty']
size, color, name = cat

# swap values without temp variable
a,b=1,2
a,b=b,a
```
### [List method](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
```
cat.index('fat') 				# 0
cat.append('lazy')
cat 						# ['fat', 'orange', 'kitty', 'lazy']
cat.insert(1, 'female')
cat 						# ['fat', 'female', 'orange', 'kitty', 'lazy']
cat.remove('kitty')
cat 						# ['fat', 'female', 'orange', 'lazy']
cat.sort()
cat.sort(reverse=True)
cat.sort(key=str.lower) 			# sorting done by ASCII upper case before lower
```

STRING : 
similar to list
big difference: string is immutable ie cannot be changed
myString = 'that is a cat named puppy'
change = ['cat','dog']
myString = myString[0:myString.index(change[0])] + change[1] + myString[myString.index(change[0]) + len(change[0]):] 
myString 					# 'that is a dog named puppy'
\' - escape

not valid in string coz immutable
del myString[5]
myString.append('.')

String Methods
str.upper(), str.lower(), str.isupper(), str.islower(), str.istitle() 		#title case
str.isalpha(), str.isalnum(), str.isdecimal(), str.isspace()
str.startswith(), str.endswith() 						# beginning and ending of string
':'.join('a','b','c') 					# a:b:c
'a:b:c'.split(':') 					# ('a','b','c')
'Hello'.rjust(10) 					# '     Hello'
'Hello'.ljust(6,'*') 					# 'Hello*' - pad left or right with spaces or string to make total of 6 characters
'Hello'.center(15,'-') 					# '-----Hello-----'
str.strip(). str.rstrip(), str.lstrip() # remove white space
'SpamSpamBaconSpamEggsSpamSpam'.strip('ampS' or 'mapS' or 'pSam')  #'BaconSpamEggs' removes all possible combination of ampS from start and end


TUPLES:
similar to list but uses () instead of []
tuples are immutable like string

tuple([ , , ]) 						# convert list to tuple
list(( , , )) 						# convert tuple to list
list('hello') 						# ['h','e','l','l','o'] - convert string to list

mutable data type like list and dictionary are stored as references/pointers

import copy
copy.copy(myList) 					# make copy of mutable data
copy.deepcopy(myList) 					# make copy of list and the inner lists

DICTIONARY:
cat = {'name': 'kitty', 'size': 'fat', 'color': 'orange', 12: 'age'}
cat['name']
Unordered
cat = {'name': 'kitty', 'size': 'fat', 'color': 'orange', 12: 'age'}
dog = {12: 'age','name': 'kitty', 'size': 'fat', 'color': 'orange'}
cat == dog 						# True

Dictionary Method:
keys(), values(), items()
for i in cat.values():
	print(i)					# just values
for i in cat.keys():
	print(i)					# just keys
for i in cat.items():
	print(i)
for k,v in cat.items():
	print('Key: ' + k + ' Value: ' + v)		# keys and values
'name' in cat.keys() 					# True
'fat' not in cat.values() 				# False
cat.get('length',0) 					# returns 0 if there is not key called length
if 'length' not in cat:	cat['length'] = '12 inch' or cat.setdefault('length', '12 inch')


pyperclip library/ package:
pyperclip.copy('Hello') 				# not as fun
pyperclip.paste() 					# paste anything in clipboard

RUN OPTIONS FROM TERMINAL:
python3 -m doctest filename.py (compile and test)
python3 -m doctest filename.py - v (in verbose mode)
python3 -i filename.py (interactive mode)

make executable from terminal (ie dont need to type python3 fileName.py)
UBUNTU
chmod +x fileName.py
WINDOWS
.bat file
@py.exe C:\myFolder\filename.py %*
@pause

pattern matching: REGULAR EXPRESSION
import re
strPattern = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')	# create regex object and use r to search as raw data
matchedObjects = strPattern.search(strBlob) 		# pass the string to search into regex object's search method
print(matchedObjects.group()) 				# call group to return the first instance of matched expression

parethesis in regular expression
strPattern = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)')	# search for regex either bracket or complete
areaCode, mainNumber = matchedObjects.groups()
matchedObjects.group(0)
areCode = matchedObjects.group(1)
matchedObjects.group(2)

matching multipe groups with |
regHero = re.compile(r'batman|wonder woman')		# finds first instace of batman or wonder woman
mo1 = regHero.search('batman, superman, wonder woman')	
mo2 = regHero.search('superman, wonder woman, batman')
mo1.group()						# returns batman
mo2.group()						# returns wonder woman

regBat = re.compile(r'bat(man|mobile|cave|girl)')
regBat = re.compile(r'bat(wo)?man')			# finds batman and batwoman. pattern in (wo)? is optional
regbat = re.compile(r'bat(wo)*man')			# finds batman, batwoman, batwowoman, batwowowoman etc
regbat = re.compile(r'bat(wo)+man')			# atleast 1 - finds batwoman, batwowoman but not batman
(Ha){3} 						# HaHaHa
(Ha){3,5}						# HaHaHa, HaHaHaHa, HaHaHaHaHa
(Ha){3, }						# Unbounded - 3 or more
(Ha){ ,5}						# Unbounded - 0 to 5

/(, /), /|, /*, /+					# searching for parethesis need escape charater even in raw string
Python regex are greedy by default 			# ie finds the longest possible string
greedyRegex = re.compile(r'(Ha){3,5}')			# finds the longest possible
nonGreedyRegex = re.compile(r'(Ha){3,5}?')		# find the shortest possible
mo1 = greedyRegex.search('HaHaHaHa')
mo2 = nonGreedyRegex.search('HaHaHaHa')
print(mo1.group() )					# HaHaHaHa
print(mo2.group() )					# HaHaHa

phoneRegex1 = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
phoneRegex2 =  re.compile(r'(\d\d\d)-(\d\d\d)-(\d\d\d\d)')
pReg1.findall('asdf ads 898-959-5265 afw da 595-898-8747') 	# ['898-959-5265', '595-898-8747'] finds all the matching exp in the string
pReg2.findall('asdf ads 898-959-5265 afw da 595-898-8747') 	# [('898', '959', '5265'), ('595', '898', '8747')] list of tuples

\d - digits 0 to 9
\D - not (digits 0 to 9)
\w - digits, letters, and underscore
\W - not (digits, letters, and underscore)
\s - space, tab, newline
\S - not (space, tab, newline)
[0-5] - matches 0,1,2,3,4,5

xReg = re.compile(r'\d+\s\w+')				# any number of digits followed by a whitespace and thena any number of words
userDef1 = re.compile(r'[aeiuoAEIOU]')			# find vowels from string
userDef2 = re.compile(r'[a-zA-Z0-9]')			# all lower and upper alpha + digits
userDef3 = re.compile(r'['[a-z.]')			# all lower and ending in period. no need \. inside []
userDef4 = re.compile(r'[^aeiuoAEIOU]')			# caret inside [] finds non regex from string
userDef5 = re.compile(r'^[a-e]+')			# caret as raw string means must start with given expression
userDef6 = re.compile(r'[a-e]+$')			# dollar sign means ends with given expression
userDef7 = re.compile(r'^d+$')				# whole string is digits
userDef8 = re.compile(r'.at')				# one wild character with dot. everything but newline
r'.*'							# more than one wild character with .*
r'.*?'							# greedy wild character with .*?

re.compile(r'ayush',re.IGNORECASE)			# case insensitive

String substitution with regex
xReg = re.compile(r'Ayush \w+')
xReg.sub('King', 'My name is Ayush Maskey')		# My name is King
censorAgents = re.compile(r'Agent (/w) w+')
censorAgents.sub('\1***', 'Agent James and Agent Bond went undercover 		# Agent J*** and Agent B*** went undercover 			

phoneRegex = re.compile(r'((\d{3}|\(\d{3}\))?(\s|-|\.)?\d{3}(\s|-|\.)\d{4}(\s*(ext|x|ext.)\s*\d{2,5})?)')
VS
phoneRegex = re.compile(r'''(							# complicated regex into readable
    (\d{3}|\(\d{3}\))?            # area code					# re.VERBOSE ignores white space and comments
    (\s|-|\.)?                    # separator					# expression inside ''' triple quote
    \d{3}                         # first 3 digits				# triple quote extends to multiple lines
    (\s|-|\.)                     # separator
    \d{4}                         # last 4 digits
    (\s*(ext|x|ext.)\s*\d{2,5})?  # extension
    )''', re.VERBOSE)


READING AND WRITING FILES
import os
os.path.join('home','amaskey','Google')						# ubuntu - home/amaskey/Google Windows - home\\amaskey\\Google 
folder= 'home/amaskey/Google'
files = ['file1.txt','file2.txtx','file3.txt']
for fileName in files:
	os.path.join(filePath, fileName)
os.getcwd()									# current working directory

open('filename')
s = set( open('~/Document.../filename').read().split() )
{w for w in s if s == s[::-1] and len(s) > 3}
{w for w in s if s[::-1] in s and len(s) == 5}

user-defined function
def fnName(parameter):
	operations
	return x

def fnName(p1, p2=100)
	ops
	return x,y
""" return more than one variable
p2=100 as default if it is not defined 
when calling the fxn"""

if 
elif
else

higher order function 
function that returns function
- function inside function
- can pass a function as parameter to a function.
def fxn1(n)
  def fxn2(k)
    return k+n+1
      return fxn2
fxn(1)(2)
- functions are first class: fxn can be manipulated as values in out programming language
- higher-order function: 
   1. a function that takes a function as an agument value 
   2. returns a function as a return value
   3. or both
use of higher-order
- express general methods of computation
- remove repition from programs
- separate concerns among functions



lambda expression
function currying
mutual recusion 
luhn sum- credit card number 
dictionary
range()
for loop

and / or short circuiting
True and 1 = 1
False and 1 = False
True or 1 = True
False or 1 = 1


functional abstraction
- need to know number of argument
- dont care about intrinsic name of function - name can be assigned to anything else. helps other humans and myself read the program
- need to know what fuction does/returns/prints
- dont care how it computes 

test driven development
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

$python3 -m doctest ex.py	#see if the test we wrote are correct


