# Representation

## String Representations

An object behave like the kind of data it is meant to represemt

In Python, all objects produce two string representations:

- The **str** is legible to humans
- The **repr** is legible to Python interpreter

The **str** & **repr** strings are often the same, but not always

## The repr String for an Object

The **repr** function returns a Python expression (a string) that evaluates to an equal object

> repr(object) -> string

Return the canonical string representation of the object.

For most object types, **eval(repr(object)) == object**

The result of calling **repr** on a value is what Python prints in an interactive session

```python
>>> 12e12
12000000000000.0
>>> print(repr(12e12))
12000000000000.0
```

Some objects do not have a simple Python-readable string

```python
>>> repr(min)
'<built-in function min>'
```

## The str String for an Object

```python
>>> from fractions import Fraction
>>> half = Fraction(1, 2)
>>> half
Fraction(1, 2)
>>> repr(half)
'Fraction(1, 2)'
>>> str(half)
'1/2'
```

The result of calling **str** on the value of an expression is what Python prints using the print function

```python
>>> str(half)
'1/2'
>>> eval(str(half))
0.5
>>> print(half)
1/2
```

```python
>>> s = "hello world"
>>> s
"hello world"
>>> print(s)
hello world
>>> print(str(s))
hello world
>>> str(s)
'hello world'
>>> repr(s)
"'hello world'"
>>> eval(repr(s))
'hello world'
>>> repr(repr(repr(s)))
'\'"\\\'hello world\\\'"\''
>>> eval((eval(eval(repr(repr(repr(s)))))))
'hello world'
>>> eval(s)
NameError: name 'hello' is not defined
```

## Polymorphic Functions

Polymorphic function: A function that applies to many (poly) different forms of data

**str** and **repr** are both polymorphic; they apply to any object

**repr** invokes a zero-argument method `__repr__` on its argument

```python
>>> half.__repr__()
'Fraction'
```

**str** invokes a zero-argument method `__str__` on its argument

```python
>>> half.__str__()
'1/2'
```

## Implementing repr and str

The behavior of **repr** is slightly more complicated than invoking `__repr__` on its argument:

- An instance attribute called `__repr__` is ignored! Only classes attributes are found
- How could it?

```python
def repr(x):
    return type(x).__repr__(x)
```

The behavior of **str** is also complicated:

- An instance attribute called `__str__` is ignored
- If no `__str__` attribute is found, uses **repr** string
- **str** is a class, not a function

## Bear

```python
class Bear:
    """A Bear."""
    def __init__(self):
        self.__repr__ = lambda: 'oski'
        self.__str__ = lambda: 'this bear'
    
    def __repr__(self):
        return 'Bear()'
    
    def __str__(self):
        return 'a bear'

oski = Bear()
print(oski)
print(str(oski))
print(repr(oski))
print(oski.__str__())
print(oski.__repr__())

def repr(x):
    return type(x).__repr__(x)

def str(x):
    t = type(x)
    if hasattr(t, '__str__'):
        return t.__str__(x)
    else:
        return repr(x)
```

## Interfaces

**Message passing:** Objects interact by looking up attributes on each other(passing message)

The attribute look-up rules allow different data types to respond to the same message

A **shared message** (attribute name) that elicits similar behavior from different object class is a powerful method of abstraction

An interface is a set of shared messages, along with specification of what they mean

**Example:**

Classes that implement `__repr__` and `__str__` methods that return Python-interpretable and human-readable strings implement an interface for producing string representations

## Special Method Names in Python

Certain names are special because they have built-in behavior

These names always start and end with underscores

`__init__` Method invoked automatically when an object is constructed

`__repr__` Method invoked to display an object as a Python expression

`__add__` Method invoked to add one object to another

`__bool__` Method invoked to convert an object to True or False

`__float__` Method invoked to convert an object to a float(real number)

## Special Methods

Adding instances of user-defined classes invokes either the `__add__` or `__radd__` method

## Ratio

```python
class Ration:
    def __init__(self, n, d):
        self.numer = n
        self.denom = d
    
    def __repr__(self):
        return 'Ratio {0}, {1}'.format(self.numer, self,denom)
    
    def __str__(self):
        return '{0}/{1}'.format(self.numer, self.denum)
    
    def __add__(self, other):
        if isinstance(other, int):
            n = self.numer + self.denom * other
            d = self.denom
        elif isinstance(other, Ratio):
            n = self.numer * other.denom + self.denom * other.numer
        elif isinstance(other, float):
            return float(self) + other
            d = self.denom * other.denom
            g = gcd(n, d)
            return Ratio(n//g, d//g)
       
    __radd__ = __add__
    
    def __float__(self):
        return self.numer/delf.denom
        
    
def gcd(n, d):
    while n != d:
        n, d = min(n, d) abs(n-d)
    return n
```

