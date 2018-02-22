# Python Trees

## Table of Content
 * [back to ToC](./table_of_content.md)
 * [python basic](./py_basics.md)
 * [Sequences - list, dict, string...](./py_sequences.md)
 * [Regular expression](./py_regular_exp.md)
 * [functions](./py_functions.md)
 * [Data Abstraction](./py_data_abstraction.md)
 * [Trees](./py_trees.md)
 * Libraries
   * [pyperclip](./py_lib_pyperclip.md)
   * [reading and writing files](./py_io.md)

## Closure
> a method for combining data values satisfies the closure property if
 * the result of combination can itself be combined using same method
 * if I can put an item into list, I should be able to take that list and put it into different list.
 * permits us to create hierarchical structures
 * Hierarchiacal structure are made up of parts, which themselves are made up of parts and so on
 * Lists can contain lists as element in addition to anything else
 * box and pointer
 
## box and pointer notation
 * lists are represented as row of index-label adjacent boxes one per element
 * each box either contains a primitive value or points to a compound value
 * pair = [1,2] --> pair is pointing to list 
 * nested_list = [ [1, 2], [], [ [3, False, None], [4, lambda:5] ] ]

## Slicing

```python
>>> odds = [3,5,7,9,11]
>>> list(range(1,3) )
[1, 2]
>>> [odds[i] for i in range(1,3)]
[5, 7]

# slicing - same as range, includes 1 but excludes 3
>>> odds[1:3]
[5, 7]
>>> odds[:3]
[3, 5, 7]
>>> odds[2:]
[7, 9, 11]
>>> odds[:]
[3, 5, 7, 9, 11]

```
## Processing container values
iterating over all the values in list or dictionary
built in functions --> Sequence aggregation

> sum(iterable [, start]) -> value
 * returns sum of iterable number plus the value of parameter start
 * start = 0 by default
 * when iterable is empty, return start

```python
>>> sum([2,3,4])
9
# can't add strings
>>> sum(['2','3','4'])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
# add start to sum of iterable
>>> sum([2,3,4], 5)
14
# adding list
>>> [2,3] + [4]
[2, 3, 4]
# start = empty list
>>> sum([[2,3],[4]], [])
[2, 3, 4]
# first one below, start with int second one start with empty list
>>> 0 + [2,3]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'list'
>>> [] + [2,3] + [4]
[2, 3, 4]
>>> 
```

> max(iterable[, key=func]) ->
> max( a, b, c, ... [, key=function]) --> value
 * return largest item for single iterable argument
 * with two or more arguments, returns the largest argument

```python
>>> max( range(5) )
4
>>> max( range(10), key=lambda x: 7 - (x-4)*(x-2) )
3
>>> (lambda x: 7 - (x-4)*(x-2) )(3)
8
>>> (lambda x: 7 - (x-4)*(x-2) )(4)
7
>>> (lambda x: 7 - (x-4)*(x-2) )(9)
-28
>>> 

```

> all(iterable) -> bool
 * return True if bool(x) is True for all values x in the iterable
 * if iterable is empty, return True

```python3
>>> bool(5)
True
>>> bool(True)
True
>>> bool(-5)
True
>>> bool(0)
False
>>> bool('hello')
True
>>> bool('')
False
>>> [x < 5 for x in range(5)]
[True, True, True, True, True]
>>> all([x < 5 for x in range(5)])
True
>>> all(range(5))
False
```
> min

> any


















