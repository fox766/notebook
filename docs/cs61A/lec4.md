# Higher Order Functions

## Assert

```python
def area(r, shape_constant):
    assert r > 0, 'A length must be positive'
    return r * r * shape_constant
```

## Higher Order Function

**Functions are first-class:** Functions can be manipulated as values in out programming language.

**Higher-order function:** A function that takes a function as an argument value or returns a function as a return value.

```python
def identity(k):
    return k

def cube(k):
	return pow(k, 3)

def summation(n, term):
    """Sum the first N terms of a sequence
    
    >>> summation(5, cube)
    225
    """
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total
def sum_naturals(n):
    """Sum the first N natural numbers
    
    >>>sum_naturals(5)
    15
    """
    return summation(n, identity)
def sum_cubes(n):
    """Sum the first N cubes of natural numbers
    
    >>>sum_cubes(5)
    225
    """
    return summation(n, cube )
```

```python
def make_adder(n):
    """Return a function that takes one argument K and       return K + N.
    
    >>> add_three = make_adder(3)
    >>> add_three(4)
    7
    >>> make_adder(4)(3)
    7
    """
    def adder(k):
        return k + n
    return adder
```

## Lambda expression

```python
>>> square = lambda x: x * x
>>> square
<function <lambda> at 0x1003c1bf8>
>>> square(4)
16
>>> (lambda x: x * x)(5)
25
>>> def square(x):
    return x * x
>>> square
<function square at 0x10293e730>
```

> lambda x: x* x

​     A function

​                    with formal parameter x

​                          that returns the value of "x * x"(must be a single expression)

*Lambda expressions in Python cannot contain statements at all.*

## Return

```python
def search(f):
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

def inverse(f):
    """Return g(y) such that g(f(x)) -> x."""
    return lambda y: search(lambda x: f(x) == y)
```

## Control

![image-20240714175602085](../assets/cs61a/image-20240714175602085.png)

## Conditional Expressions

A conditional expression has the form 

​            <consequent> if <predicate> else <alternative>

Evaluation rule:

1. Evaluate the <predicate> expression.
2. If it's a true value, the value of the whole expression is the value of <consequent>
3. Otherwise, the value of the whole expression is the value of <alternative>

```python
>>> x = 0
>>> abs(1/x if x != 0 else 0)
0
```

