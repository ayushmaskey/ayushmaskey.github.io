# Python Functions

## Table of Content
 * [back to ToC](./table_of_content.md)
 * [python basic](./py_basics.md)
 * [Sequences - list, dict, string...](./py_sequences.md)
 * [Regular expression](./py_regular_exp.md)
 * [functions](./py_functions.md)
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
     * [order of recursion](#order-of-recursion)
     * [tree recursion](#tree-recursion)
       * [counting partition](#counting-partition)
     * [mutual recursion](#mutual-recursion)
     * [converting recursion to iteration](#converting-recursion-to-iteration)
     * [converting iteration to recursion](#converting-iteration-to-recursion)
   * [functional abstraction](#functional-abstraction)
   * [test driven development](#test-driven-development)
   * [function currying](#function-currying)
   * [function decorators](#function-decorators)
 * [Data Abstraction](./py_data_abstraction.md)
 * [Trees](./py_trees.md)
 * Libraries
   * [pyperclip](./py_lib_pyperclip.md)
   * [reading and writing files](./py_io.md)


## Functions
 * Domain --> set of all possible inputs
 * Range --> set of all possible outputs
 * give each function exactly one job --> sissor not swiss army knife
 * dont repeat yourself (DRY) --> implement process once but execute many times
 * define function generally --> one general way to plug into scoket instead for 2 ppin, 2 pin etc etc

```python
# dynamic function??
>>> exec('curry = lambda f: lambda x: lambda y: f(x,y)')
>>> curry
<function <lambda> at 0x7f05452439d8>
>>> curry(sum)(1)(2)
>>> from random import randint
>>> curry(randint)(3)(58)
45
>>> 
```
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
> a function that calls itself

```python
# sum digits without loop

def split(n):
	""" return positive n into all but its last digit and it last digit"""
	return n // 10, n % 10

# base cases - without recursive. very simple problem
# recursive case - call itself with simpler form of problem until we reach base case

def sum_digit(n):
	"""return sum of digits of positive integer n"""
	if n < 10:
		return n
	else:
		all_but_last, last = split(n):
		return sum_digit(all_but_last) + last
```
** recursive leap of faith**
1. verify base case
2. Treat fact as functional abstraction
3. Assume that fact(n-1) is correct
4. Verify that fact(n) is correct, assuming that fact(n-1) correct

## mutual recursion 

* luhn sum- credit card number 
 * last number is check sum of first 15
 * starting 15th moving left, double the value of every second digit
 * if if double returns greater than 9, sum the digits of product
 * take sum of all the digit = n * 10 (multiple of 10)
 * odd numbers get doubled.
 * 16th is checksum - to make luhn sum multiple of 10

```python
# two functions call each other
# base case can be in one or both

def split(n):
	""" return positive n into all but its last digit and it last digit"""
	return n // 10, n % 10
def luhn_sum(n):
	if n < 10:
		return n
	else: all_but_last = split(n):
		return luhn_sum_double(all_but_last) + last

def luhn_sum_double(n):
	all_but_last, last = split(n)
	luhn_digit = sum_digit(2 * last)
	if n < 10:
		return luhn_digit
	else:
		return luhn_sum(all_but_last) + luhn_digit

```

## converting recursion to iteration
* iteration is special case of recursion
* figure out what state must be maintained by iterative function

## converting iteration to recursion
*  state of iteration can be passed as arguments

## order of recursion
```python
def cascade(n):
	if n < 10:
		print(n)
	else:
		print(n)
		cascade(n // 10)
		print(n)

>>> cascade(3)
3
>>> cascade(321)
321		#print before cascade recusion - call before recursion
32		#print before cascade recusion - call after first recursion
3		#print in base case
32		#print after cascade recusion - call after first recursion
321		#print after cascade recusion - call before recursion
>>> 


def cascade1(n):
	print(n)
	if n > 10:
		cascade(n // 10)
		print(n)
#same result
```
* separating base case and recursive case is better

```python
def inverse_cascade(n):
	""" inverse cascade
	>>>inverse_cascade(123)
	1
	12
	123
	12
	1
	"""
	grow(n)
	print(n)
	shrink(n)

def f_then_g(f, g, n):
	if n:
		f(n)
		g(n)

grow = lambda n: f_then_g(grow, print, n//10)
shrink = lambda n: f_then_g(print, shrink, n//10)

>>> inverse_cascade(321)
3
32
321
32
3
>>> 
```

## tree recursion
* tree shaped processes arises whenever executing the body of recursive makes more than one call to the function
* fibonacci

```python
def fib(n):
	if n == 0:
		return 1
	elif n == 1:
		return 1
	else:
		return fib(n-2) + fib(n-1)
# this one very slow. no memoization
```

## counting partition
```python
def count_partitions(n, m):
	if n == 0:
		return 1
	elif n < 0:
		return 0
	elif m == 0:
		return 0
	else:
		with_m = count_partitions(n-m, m)
		without_m = count_partitions(n, m-1)
		return with_m + without_m
>>> count_partitions(5,3)
5
>>> 
# number of ways to add to 5 using 3 or less
# 1+1+1+1+1 = 5
# 1+1+1+2   = 5
# 1+2+2     = 5
# 1+1+3     = 5
# 2+3       = 5
```

## functional abstraction

```python
def square(x):
	return mul(x, x)

def sum_squares(x,y):
	return square(x) + square(y)
```
> what does sum_squares need to know about squares?
  * square takes one argument: yes
  * square has the intrinic name square: no, intrinsic name is only for human
  * square computes square of number: yes
  * square computes the square by calling mul: no

> choosing names
  * name dont matter for correctness but matter for composition. other human readable
  * name should convey meaning or purpose of values to which they are bound
  * the types of value bound to the name is best documented in a function's docstring
  * function name typically convey their effect (print), their behavior (triple) or value returned (abs)

> which values deserve a name
  * repeated compound expression
  * pull out meaningful part of compound statement if compound statement is too complex

## test driven development
> write test before writing a function
  * test will clarify the domain, range and behavior of a function
  * test can help identify tricky edge cases
> develop incrementally and test each piece before moving on.
  * cant depend on code that hasn't been tested
  * run your old tests again after you make new changes
> run your code interactively
  * dont be afraid to experiment with a function after you write it
  * interactive sessions can become doctests. just copy and paste 

```python
from ucb import trace	# create my own trace for testing 

@trace  	#trace decorator function is doing instead of prints everywhere
def gcd(n,m):
  """
  >>> gcd(12,8)
  4
  >>>find all possible cases
  """
  if m == n:
	return m:
  elif m < n:
	return gcd(n, m)
  else return gcd(m-n, n)
```

## function currying 
> way of manipulating function
  * there's a general relationship between these functions

> currying: 
  * transforming a multi-argument function into single-argument, higher order function
  * it returns a function that takes rest of the argument

```python
def make_adder(n):
	return lambda k: n + k

>>> make_adder(2)(3)
5
>>> add(2,3)
5


def curry2(f):
	def g(x):
		def h(y):
			return f(x,y)
		return h
	return g
>>> from operator import add
>>> add(2,3)
5
>>> m = curry2(add)
>>> m(2)(3)
5
>>> add_three = m(3)
>>> add_three(2)
5

#define as lambda expression
>>> curry3 = lambda f: lambda x: lambda y: f(x,y)
>>> m = curry3(add)
>>> m(3)(4)
7
>>> add_four = m(4)
>>> add_four(3)
7
>>> 
```

## function decorators
```python3
def trace1(fn):
	"""Returns a version of fn that first prints before it is called
	
	fn - a function of 1 argument
	"""
	def traced(x):
		print("calling", fn, "on argument", x)
		return fn(x)
	return traced

@trace1
def square(x):
	return x * x

def sum_squares_up_to(n):
	k = 1
	total = 0
	while k <= n:
		total, k = total + square(k), k + 1
	return total

>>> square(2)
calling <function square at 0x7f3264c297b8> on argument 2
4
>>> sum_squares_up_to(5)
calling <function square at 0x7f3264c297b8> on argument 1
calling <function square at 0x7f3264c297b8> on argument 2
calling <function square at 0x7f3264c297b8> on argument 3
calling <function square at 0x7f3264c297b8> on argument 4
calling <function square at 0x7f3264c297b8> on argument 5
55
>>> 
```
> better version of trace1 in implemented usb in hog
  * from usn import trace

> shortcut transforming a function in another function 
  * use annotation like @trace
  * called decorator
  * @trace1 : decorator
  * def square(): decorated function

```python3
@trace1
def triple(x):
  return 3 * x

# is identical to

def triple(x):
  return 3 * x
triple = trace1(triple)

# nice to know what decoration applied so use decorator
```


