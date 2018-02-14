# Python Data Abstraction

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


## Data Abstraction

> compound objects combine objects together
 * a date: a year, month and day
 * geographic position: latitude and longitude
 * abstract data type lets us manipultaes compound objects as units
 * Isolate two parts of any program that uses data
   * how data are represented (as parts)
   * how data are manipulated ( as units)
> data abstraction: 
 * a methodology by which functions enforce an abstraction barrier between representation and use
 
## rational number
> numerator / denominator
 * exact representation of fractions
 * a pair of integers
 * as soon as division occers, exact representation may be lost
   * rational(n, d) returns a rational number x
   * numer(x) returns numerator of x
   * denom(x) returns denominator of x
     * rational --> constructor
     * numer and denom --> selector

```python
from fractions import gcd

def rational(n, d):
	"""construct a rational number that represents N/D"""
	g = gcd(n, d)
	return [n // g, d // g]

def numer(x):
	"""Return the numerator of rational number x"""
	return x[0]

def denom(x):
	"""Return the denominator of rational number x"""
	return x[1]

def mul_rational(x, y):
	return rational(numer(x) * numer(y), denom(x) * denom(y))

def add_rational(x, y):
	nx, dx = numer(x), denom(x)
	ny, dy = numer(y), denom(y)
	return rational(nx * dy + ny * dx, dx * dy)

def equal_rational(x,y):
	return numer(x) * denom(y) == numer(y) * denom(x)

def print_rational(x):
   	"""print rational x """
	print ( numer(x), "/", denom(x) )

>>> x, y = rational(1,2), rational(3,8)
>>> print_rational(mul_rational(x, y) )
3 / 16

```
 * define all the ways to manipulate rational numbers in terms of three functions
 * these function implement abstract data type for rational numbers
 * rational number is pair of integers
 * change definition of rational changes
   * before it whatever the result
   * now reduce to lowest term 
      * only change the function rational. 
      * all other functions remain same.
      * benefit of data abstraction

## abstraction barriers
 * separate different part of program
 * each part only knows so much about the rest of the program
 * allows change in one part of program without breaking the rest

top layer --> computation --> treat data values as whole --> eg add_rational, mul_rational

=================abstraction barrier====================================

second layer --> create and implement rational --> numerators and denominators --> eg. rational, numer, denom

=================abstraction barrier====================================

third layer --> implement selector and constructor --> two element lists --> list liternal and element selection

=================abstraction barrier====================================

implementation of list --> we dont know how python implements list and we don't care


> abstraction barrier
 * dont use second layer to do camputations. always top layer
 * when building numer function, it should not know where it is list or array in third layer
 * if abstraction layer is not crossed, easy to change in future

```python
def divide_rational_violate_abstraction(x, y):
	return [ x[0] * y[1], x[1] * y[0] ]

add_rational( [1, 2], [1, 4])
```
> violations
 * calling add_rational does not use constructors
 * divide --> no selector. should not assume it is list

**can change data representaion without having to rewrite entire program**

## data representation

 * for some reason rational constructor has to change

```python3
def rational(n, d):
	"""construct a rational number that represents N/D"""
	def select(name):
		if name == 'n':
			return n
		elif name == 'd':
			return d
	return select

def numer(x):
	"""Return the numerator of rational number x"""
	return x['n']

def denom(x):
	"""Return the denominator of rational number x"""
	return x['d']
```

 * constructors and selectors --> rational, numer and denom has changed
 * but no need to change operatives --> add_rational, mul_rational



