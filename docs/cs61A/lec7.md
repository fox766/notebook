# Function Example

```python
# Implementing a Function
def remove(n, digit):
    """Return all digits of non-negative N that are not   
    DIGIT, for some non-negative DIGIT less than 10.
    >>> remove(231, 3)
    21
    >>> remove(243132, 2)
    4313
    """
    kept, digits = 0, 0
    while __________:
        n, last = n // 10, n % 10
        if _______________:
            kept = _____________
            digits = ____________
    return _________________
```

*solution:*

(1) 10 ** digits

(2) kept = kept / 10 + last

## Decorating

```python
def trace1(fn):
    """Returns a version of fn that first printed     
    before it is called.
    fn - a function of one argument
    """
    def traced(x):
        print('Calling', fn, 'on argument', x)
        return fn(x)
    return traced

@trace1
def square(x):
    return x * x

"""
def square(x):
    return x * x
square = trace1(square)
"""

@trace1
def sum_squares_up_to(n):
    k, total = 1, 0
    while k <= n:
        total, k = total + square(k), k + 1
    return total
```

## Previous Exam Examples

```python
def repeat(k):
    """When called repeatedly, print each repeated argument.
    >>> f = repeat(1)(7)(7)(3)(4)(2)(5)(1)(6)(5)(1)
    7
    1
    5
    1
    """
    return ___detector(lambda j: False)___(k)

def detector(f):
    def g(i):
        if __f(i)__:
            __print(i)___
        return __detector(lambda j == i or f(i))___
    return g

# it's more reasonable to rename f as have_seen_before
```

