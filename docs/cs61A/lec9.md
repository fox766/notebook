# Tree Recursion

## Cascade

```python
def cascade(n):
    if n < 10:
        print(n)
    else:
        print(n)
        cascade(n//10)
        print(n)
>>> cascade(1234)
1234
123
12
1
12
123
1234

def inverse_cascade(n):
    grow(n)
    print(n)
    shrink(n)

def f_then_g(f, g, n):
	if (n):
        f(n)
        g(n)

grow = lambda n: f_then_g(grow, print, n//10)
shrink = lambda n: f_then_g(print, shrink, n//10)
>>> inverse_cascade(1234)
1
12
123
1234
123
12
1
```

## Tree Recursion

> Tree-shaped processes arise whenever executing the body of a recursive function makes more than one call to that function.

## Counting Partitions

```python
def count_partitions(n, m):
    if n == 0:
        return 1
    elif n < 0:
        return 0
    elif m == 0:
        return 0
    else:
        with_m = count_partitons(n-m, m)
        without_m  = count_partitions(n, m-1)
        return with_m + without_m
```

