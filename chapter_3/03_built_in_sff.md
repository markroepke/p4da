# Chapter 3) Built-in Data Structures, Functions, and Files

The chapter covers the built-in data funcitonality of Python. Libraries like pandas and NumPy build off the material in this chapter. We will start with common data structures:

* tuples
* lists
* dicts
* sets

Then custom functions will be covered, followed by interacting with the local hard drive.

## 3.1 Data Structures and Sequences

### Tuple

A tuple is a fixed-length sequence of Python objects. Tuples are immutable. Tuples can be created with a comma-separated sequence of values:

```python
In [1]: tup = 4, 5, 6

In [2]: tup
Out[2]: (4, 5, 6)
```

Enclosing the values of a tuple with parentheses can be helpful when making more complex objects:

```python
In [1]: nested_tup = (1, 2), (3, 4, 5)

In [2]: nested_tup
Out[2]: ((1, 2), (3, 4, 5)) 
```

You can convert any sequence into a tuple by using the `tuple()` function.

Elements of a tuple can be accessed using brackets (`[]`). Note that elements are indexed starting from zero in Python, versus starting with one in R.

```python
In [1]: tup = (1, 2, 3)

In [2]: tup[1]
Out[3]: 2
```

Note that tuples themselves are immutable, but if an element of a tuple is a mutable object they can be mutated in place:

```python
In [1]: tup = tuple(['foo', [1, 2], True])

In [2]: tup[2] = False
------------------------------------------
TypeError ...
```

```python
In [1]: tup = tuple(['foo', [1, 2], True])

In [2]: tup[1].append(3)

In [3]: tup
Out[3]: ('foo', [1, 2, 3], True)
```

Tuples can be concatenated like strings, using the `+` operator:

```python
In [1]: (1, 2, 3) + (4, 5)
Out[1]: (1, 2, 3, 4, 5)
```

If you multiple a tuple by an `x`, `x` copies of the tuple will be concatenated together. While this is the same as Python lists, not that this is very different from the vectorized behavior of R.

```python
In [1]: tup = 1, 2, 3

In [2]: tup * 2
Out[2]: (1, 2, 3, 1, 2, 3)
```

#### Unpacking tuples

Python will try to *unpack* tuples when they are assigned to a tuple-like expression of variables:

```python
In [1]: tup = (1, 2, 3)

In [2]: a, b, c = tup

In [3]: a
Out[3]: 3
```

A common use of variable unpacking is when iterating over sequences of tuples or lists:

```python
In [1]: seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]

In [2]: for a, b, c in seq:
  ....:     print('a={0}, b={1}, c={2}'.format(a, b, c))
a=1, b=2, c=3
a=4, b=5, c=6
a=7, b=8, c=9
```

#### Tuple methods

Since tuples are immutable, there are few methods available. A useful one is `count()`, which counts the occurrences of a value:

```python
In [1]: tup = (1, 2, 3, 4, 5, 5, 5)

In [2]: tup.count(5)
Out[2]: 3
```
