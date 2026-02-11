# Environments

*Review the exp:*

```python
def make_adder(n):
    def adder(k):
        return k + n
    return adder

add_three = make_adder(3)
add_three(4)
make_adder(3)(4)
```

Looking at the environment diagram of this:

![image-20240715092531819](../assets/cs61a/image-20240715092531819.png)

Note that the parent of adder is make_adder. The parent of a function is the frame which is was defined.

##  Self Reference

```python
def print_all(x):
    print(x)
    return print_all

>>> print_all(1)(3)(5)
1
3
5
```

```python
def print_sums(n):
    print(n)
    def next_sum(k):
        return print_sums(n+k)
    return next_sum

>>> print_sums(1)(3)(5)
1
4
9
```

## Curry

```python
def curry2(f):
    def g(x):
        def h(y):
            return f(x, y)
        return h
    return g

# curry2 <=> lambda f: lambda x: lambda y: f(x, y)
>>> m = curry2(add)
>>> m(2)(3)
5
>>> add(2, 3)
5
```

**Currying:** Tranforming a multi-argument function into a single-argument, higher-order function.