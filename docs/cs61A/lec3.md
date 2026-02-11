# Control

```python
>>> print(print(1), print(2))
1
2
None None
```

```python
>>> from operator import truediv, floodiv, mod
>>> truediv(2013, 10)
>>> 201.3
>>> floordiv(2013, 10)
>>> 201
```

```python
>>> def divide_exact(n, d=10): #default choices
    return n // d, n % d
>>> quotient, remainder = divide_exact(2013, 10)
>>> quotient
201
>>> remainder
3
>>> q, r = divide_exact(2013)
>>> q
201
>>> r
3
```

## Boolean Contexts

False values in python: 0, '', False, None (more to come)

True values: Anything else

## While Statement

exp:

```python
def smallest_prime_factor(n):
    """Find the smallest factor of n."""
    k = 2
    while n % k != 0:
        k += 1
    return k

def prime_factors(n):
    """Print the prime factors of n in non_decreasing order.
    
    >>> prime_factors(8)
    2
    2
    2
    >>> prime_factors(858)
    2
    3
    11
    13
    """
    while n > 1:
        k = smallest_prime_factor(n)
        n = n // k
        print(k)
```

