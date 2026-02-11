# Data Example

## Land Owners

![image-20240922230449258](../assets/cs61a/image-20240922230449258.png)

## Example: using built-in function & Comprehensions 

```python
def min_abs_indices(s):
    """Return the indices of all elements in a list S with the smallest absolute value."""
    min_abs = min(map(abs, s))
    f = lambda i: abs(s[i]) == min_abs
    return list(filter(f, range(len(s))))

def largest_adj_sum(s):
    """Largest sum of two adjacement elements in a list S."""
    return max([a + b for a, b in zip(s[:-1], s[1:])])

def digit_dict(s):
    """Map each digit d to the lists of elements in S that end with d.
    >>> digit_dict([5, 8, 13, 21, 24, 55, 89])
    {1:[21], 3:[13], 4:[34], 5:[5, 55], 8:[8], 9:[89]}
    """
    # a dictionary comprehension
    return {d:[x for x in s if x % 10 == d] for d in range(10) if any([x % 10 == d for x in s])}

def all_have_an_eaual(s):
    """Does every element equal some other element in S."""
    # return all(s[i] in s[:i]+s[i:] for i in range(s))
    # return all([sum([1 for y in s if y == x]) > 1 for x in s])
    return min(s.count(x) for x in s) > 1
```

## Examples: Linked Lists

```python
def ordered(s, key = lambda x: x):
    """Is Link S ordered?"""
    if s is Link.empty or s.rest is Link.empty:
        return True
    elif key(s.first) > key(s.rest.first):
        return False
    else:
        return ordered(s, key)

def merge(s, t):
    """Return a sorted Link with the elements of sorted S and sorted T."""
    if s is Link.empty:
        return t
    elif t is Link.empty:
        return s
    elif s.first <= t.first:
        return Link(s.first, merge(s.rest, t))
    else:
        return Link(t.first, merge(s, t.rest))
    
def merge_in_place(s, t):
    """Never call Link."""
    if s is Link.empty:
        return t
    elif t is Link.empty:
        return s
    elif s.first <= t.first:
        s.rest = merge_in_place(s.rest, t)
        return s
        # return Link(s.first, merge(s.rest, t))
    else:
        t.rest = merge_in_place(s, t.rest)
        return t
        # return Link(t.first, merge(s, t.rest))
    
```

