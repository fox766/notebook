# Trees

## The Closure Property of Data Types

1. A method for combining data values satisfies the *closure property* if: The result of combination can itself be combined using the same method (like putting lists into a list)
2. Closure（闭包） is powerful because it permits us to create hierarchical structures（层次结构）
3. Hierarchical structures are made up of parts which themselves are made of parts, and so on

## Box-and-Pointer Notation in Environment Diagram

Lists are represented as a row of index-labeled adjacent boxes, one per element.

Each box either contains a primitive value or points to a compound value.

![image-20240730112056324](../assets/cs61a/image-20240730112056324.png)

## Slicing

```python
digits = [1, 8, 2, 8]
start = digits[:1]
middle = digits[1:3]
end = digits[2:]
```

## Sequence Aggregation

> **sum**(iterable[, start]) -> value

Return the sum of an iterable of numbers (**Not Strings**) plus the value of parameter 'start' (which defaults to 0). When iterable is empty, return start.

```python
>>> sum([2, 3, 4])
9
>>> sum([2, 3, 4], 5)
14
>>> sum(['2', '3', '4'])
TypeError: unsupported operand type(s) for+: 'int' and 'str'
>>> sum([[2, 3], [4]], [])
[2, 3, 4]
>>> sum([[2, 3], [4]])
TypeError: unsupported operand type(s) for+: 'int' and 'list'
>>> sum(['2', '3', '4'], '')
TypeError: sum() can't sum strings [use ''.join(seq) instead]
>>> sum([ [[1]], [2] ], [])
[[1], 2]
```

> **max**(iterable[, key = func]) -> value            \min
>
> **max**(a, b, c, ...[, key = func]) -> value           \min

With a single iterable argument, return its largest item.

With two or more arguments, return the largest argument.

```python
>>> max(range(10), key=lambda x: 7-(x-4)*(x-2))
3
>>> max([3, 8], [4, 5])
[4, 5]
```

> **all**(iterable) -> bool                                        \any

Return True if bool(x) is True for all values x in the iterable. If the iterable is empty, return **Ture**.

```python
>>> all([x < 5 for x in range(5)])
Ture
```

## Trees

### Tree Abstraction --- Two Descriptions

![image-20240730115626662](../assets/cs61a/image-20240730115626662.png)

"Each parent is the sum of its children" is ture for a fibonacci tree.

### Implementing The Tree Abstraction

![image-20240730141945054](../assets/cs61a/image-20240730141945054.png)

```python
def tree(label, branches=[]):
    for branch in braches:
        assert is_tree(brach), 'branches must be trees'
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

def fib_tree(n):
    if n <= 1:
        return tree(n)
    else:
        left, right = fib_tree(n-2), fib_tree(n-1)
        return tree(label(left)+label(right), [left, right])

def count_leaves(t):
    """Count the leaves of a tree."""
    if is_leaf(t):
        return 1
    else:
        sum([count_leaves(b) for b in branches(t)])
        
def leaves(tree):
    """Return a list containing the leaf labels of the tree.
    >>> leaves(fib_tree(5))
    [1, 0, 1, 0, 1, 1, 0, 1]
    """
    if is_leaf(tree):
        return [label(tree)]
    else:
        return sum([leaves(b) for b in braches(tree)], [])

# create trees
def increment_leaves(t):
    """Return a tree like t but with labels incremented."""
    if is_leaf(t):
        return tree(label(t)+1)
    else:
        bs = [increment_leaves(b) for b in branches(t)]
        return tree(label(t), bs)

def increment(t):
    """Return a tree like t but with all labels incremented."""
    return tree(label(t)+1, [increment(b) for b in branches(t)])

# print trees
def print_tree(t, indent=0):
    print('  '*indent+str(label(t)))
    for b in branches(t):
        print_tree(b, indent+1)
        
# sum from leaves to root
def print_sums(t, so_far):
    so_far += label(t)
    if is_leaf(t):
        print(so_far)
    else:
        for b in branches(t):
            print_sums(b, so_far)

```

