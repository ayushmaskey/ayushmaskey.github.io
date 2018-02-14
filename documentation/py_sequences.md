# Python Sequences 

## Table of Content
 * [back to ToC](./table_of_content.md)
 * [python basic](./py_basics.md)
 * [Sequences - list, dict, string...](./py_sequences.md)
   * [Array](#array)
   * [List basic](#list-basic)
     * [List method](#list-method)
     * [pair](#pair)
   * [String basic](#string-basic)
     * [String methods](#string-methods)
   * [Tuples](#tuples)
   * [Dictionary](#dictionary)
     * [Dictionary method](#dictionary-method)
 * [Regular expression](./py_regular_exp.md)
 * [reading and writing files](./py_io.md)
 * [functions](./py_functions.md)
 * [Data Abstraction](./py_data_abstraction.md)
 * [Trees](./py_trees.md)
 * Libraries
   * [pyperclip](./py_lib_pyperclip.md)


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

# mutable data type like list and dictionary are stored as references/pointers
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
## pair
 * consists of two value that are bundled in such a way that you can consider them as whole
 * representing pair --> built-in example list
 * a list liternal is comma separated expression in brackets

```python
>>> pair = [2,3]
>>> pair
[2, 3]
>>> x, y = pair

# unpack list
>>> x
2
>>> y
3
>>> pair[0]
2
>>> pair[1]
3

# unpack list using fuction.
>>> from operator import getitem
>>> getitem(pair, 0)
2
>>> getitem(pair, 1)
3
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

```python
>>> 'here' in "where's waldo?"
True
>>> 
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
>>> for i in cat.values():
...     print(i)
... 
age
kitty
orange
fat
>>> 


# just keys
>>> for i in cat.keys():
...     print(i)
... 
12
name
color
size
>>> 

#both keys and values
>>> for i in cat.items():
...     print(i)
... 
(12, 'age')
('name', 'kitty')
('color', 'orange')
('size', 'fat')
>>> 

>>> cat.keys()
dict_keys([12, 'name', 'color', 'size'])
>>> cat.values()
dict_values(['age', 'kitty', 'orange', 'fat'])
>>> cat.items()
dict_items([(12, 'age'), ('name', 'kitty'), ('color', 'orange'), ('size', 'fat')])
>>> cat
{12: 'age', 'name': 'kitty', 'color': 'orange', 'size': 'fat'}
>>> 


# keys and values
for k,v in cat.items():
	print('Key: ' + k + ' Value: ' + v)

# search for key in dictionary
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

# dictionary comprehension
>>> squares = {x: x*x for x in range(10)}
>>> squares
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81}
>>> squares[7]
49
>>> 
```
> restriction
 * cant have duplicate keys
 * key can have list
 * key cannot be list or dictionary
 * unordered
