# Python IO

## Table of Content
 * [back to ToC](./table_of_content.md)
 * [python basic](./py_basics.md)
 * [Sequences - list, dict, string...](./py_sequences.md)
 * [Regular expression](./py_regular_exp.md)
 * [reading and writing files](./py_io.md)
 * [functions](./py_functions.md)
 * [Data Abstraction](./py_data_abstraction.md)
 * [Trees](./py_trees.md)
 * Libraries
   * [pyperclip](./py_lib_pyperclip.md)

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

## try-except
```python
try:
  return 42/x
except ZeroDivisionError:			#if x == 0
  print('Bad Input')
```
