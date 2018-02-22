# Python Trees

* root / branch / node with value 
* parent / child / ancenstors / decendents / siblings
* each branch is a tree
* tree with 0 branch is leaf

## implementing tree abstraction
> tree(3, [tree(1), tree(2, [tree(1), tree(1)])])

```python3

# by default empty tree coz branch is empty list
# convert branch to list before add to label list
def tree(label, branches=[]):
	for branch in branches:
		assert is_tree(branch), "branches must be tree"
	return [label] + list(branches)

def label(tree):
	return tree[0]

def branches(tree):
	return tree[1:]

def is_tree(tree):
	if type(tree) != list or len(tree) < 1:
		return False
	for branch in branches(tree):
		if not is_tree(branch):
			return False
	return True

def is_leaf(tree):
	return not branches(tree)

>>> tree(1)
[1]
>>> is_leaf(tree(1))
True
>>> is_tree(tree(1))
True
>>> t = tree(1, [tree(5, [tree(7)]), tree(6)] )
>>> t
[1, [5, [7]], [6]]
>>> label(t)
1
>>> branches(t)
[[5, [7]], [6]]
>>> branches(t)[0]
[5, [7]]
>>> is_tree(branches(t)[0])
True
>>> label(branches(t)[0])
5
```


## Tree Processing
```python3
# build fibonacci tree

def fib_tree(n):
	if n <= 1:
		return tree(n)
	else:
		left, right = fib_tree(n-2), fib_tree(n-1)
		return tree(label(left) + label(right), [left, right])

def count_leaves(t):
	"""count the laeves of tree"""
	if is_leaf(t):
		return 1
	else:
		branch_counts = [count_leaves(b) for b in branches(t)]
		return sum(branch_counts)

def leaves(tree):
	"""Returns a list containing the leaf labels of tree

	>>> leaves(fib_tree(5))
	[1, 0. 1, 0, 1, 1, 0, 1]
	"""
	if is_leaf(tree):
		return [label(tree)]
	else:
		return sum([leaves(b) for brances(tree)],[] )

def increment_leaves(t):
	"""Return a tree like t but with lead labels incremented"""
	if is_leaf(t):
		return tree(label(t) + 1)
	else:
		bs = increment_leaves( [leaves(b) for brances(tree)] )
		return tree(label(t) + bs)

def increment(t):
	"""Return a tree like t but with all labels incremented"""
	return tree( label(t) + 1, [increment(b) for b in brances(tree)] )

def print_tree(t, indent=0):
	print(' ' * indent + str(label(t)) )
	for b in branches(t):
		print_tree(b, indent+1)

>>> fib_tree(2)
[1, [0], [1]]
>>> fib_tree(1)
[1]
>>> fib_tree(0)
[0]
>>> fib_tree(4)
[3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]
>>> label(fib_tree(4))
3
>>> count_leaves(fib_tree(4))
5
>>> count_leaves(fib_tree(10))
89
>>> fib_tree(10)
[55, [21, [8, [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]], [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]]], [13, [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]], [8, [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]], [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]]]]], [34, [13, [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]], [8, [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]], [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]]]], [21, [8, [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]], [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]]], [13, [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]], [8, [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]], [5, [2, [1], [1, [0], [1]]], [3, [1, [0], [1]], [2, [1], [1, [0], [1]]]]]]]]]]
>>> 
>>> print_tree(fib_tree(4))
3
 1
  0
  1
 2
  1
  1
   0
   1
>>> 
```


