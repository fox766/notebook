# Containers

## Lists

```python
>>> odds = [41, 43, 47, 49]
>>> len(odds)
4
>>> odds[odds[3]-odds[2]]
47
>>> digits = [1, 8, 2, 8]
>>> digits[3] <=> getitem(digits, 3)
>>> [2, 7] + digits * 2 <= add([2, 7], mul(digits, 2))
# Nested Lists
>>> pairs = [[10, 20], [30, 40]]
>>> pairs[1]
[30, 40]
>>> pairs[1][0]
30
```

## Containers

```python
# in just go from element to element
>>> digits = [1, 8, 2, 8]
>>> 1 in digits
True
>>> '1' in digits
False
>>> [1, 8] in digits
False
>>> [1, 2] in [1, [1, 2], 3]
True
```

## For Statement

```python
def count(s, value):
    """Count the number of times taht value appears in the sequence of s.	
    >>> count([1, 2, 1, 2, 1], 1)
    3
    """
    total = 0
    for elements in s:
        if element == value:
            total += 1
    return total
```

## Sequence Unpacking

```python
>>> pairs = [[1, 2], [2, 2], [3, 2], [4, 4]] # -> A sequence of fixed-length sequences
>>> same_count = 0
>>> for x, y in pairs: # x, y are bound to the element in the fixed-length sequence, as in multiple assignment.
    if x == y:
        same_count = same_count + 1
>>> same_count
2
```

## Range

A range is a sequence of consecutive integers.

```python
>>> list(range(4))
[0, 1, 2, 3]
>>> range(5, 8)
range(5, 8)
def cheer():
    for _ in range(3): # _ means you don't care actually it is.
        print('Go Bears!')
```

## Lists Comprehension

```python
>>> odds = [1, 3, 5, 7, 9]
>>> [x+1 for x in odds]
[2, 4, 6, 8, 10]
>>> [x for x in odds if 25 % x == 0]
[1, 5]
def divisors(n):
    return [1] + [x for x in range(2, n) if n%x==0]
```

## Strings

```python
>>> 'curry = lambda f: lambda x: lambda y: f(x, y)'
>>> exec('curry = lambda f: lambda x: lambda y: f(x, y)')
>>> curry
<function <lambda> at 0x....>
>>> 'I am string'
'I am string'
>>> "I've got an apostrophe" # single-quoted and double-quoted strings are equivalent
"I've got an apostrophe"
>>> """The Zen of Python
claims, Readability counts."""
'The Zen of Python\nclaims, Readability counts.'
# bacKslash n means line feed, representing a new line.
```

## Strings are Sequences

```python
>>> city = 'Berkeley'
>>> len(city)
8
>>> city[3]
'k'
# It returns a string.
# However, the "in" and "not in" operators match substrings.
>>> 'here' in "Where's Waldo?"
True
```

## Reverse a string

reverse("ward") = reverse("ard") + "w"

```python
def reverse(s):
    if len(s) == 1:
        return s
    else:
        return reverse(s[1:]) + s[0]
```

