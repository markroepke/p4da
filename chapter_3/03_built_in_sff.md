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

### List

Lists are also sequences of Python objects, but they are variable-length and can be modified in-place. They can be defined with `[]` or `list()`:

```python
In [1]: lst_a = [1, 2, 3]

In [2]: lst_b = list(1, 2, 3)
```

Lists and tuples are semantically similar and can be interchanged in many functions. The `list()` function is used frequently to create an iterator:

```python
In [1]: gen = range(10)

In [2]: gen
Out[2]: range(0, 10)

In [3]: list(gen)
Out[3]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### Adding and removing elements

The `append()` method can be used to add elements to the end of a list:

```python
In [1]: lst = ['a', 'b', 'c']

In [2]: lst.append('d')
Out[2]: ['a', 'b', 'c', 'd']
```

The `insert()` method can be used to insert an element in a particular position of a list:

```python
In [1]: lst = ['a', 'c', 'd']

In [2]: lst.insert(1, 'b')
Out[2]: ['a', 'b', 'c', 'd']
```

Note that `insert()` is computationally expensive. The `pop` method removies and returns an element at a particular index:

```python
In [1]: lst = ['a', 'b', 'c', 'd']

In [2]: lst.pop(1)
Out[2]: 'b'

In [3]: lst
Out[3]: ['a', 'c', 'd']
```

Elements of a list can be removed with `remove()`. Note that only the first such value is removed.

```python
In [1]: lst = ['a', 'b', 'c', 'b']

In [2]: lst.remove('b')

In [3]: lst
Out[3]: ['a', 'c', 'b']
```

You can check if a list contains a value using `in`:

```python
In [1]: lst = ['a', 'b', 'c']

In [2]: 'a' in lst
Out[2]: True

In [3]: 'a' not in lst
Out[3]: False
```

Note that `in` is slow with lists relative to dicts and sets which will be introduced soon.

#### Combining and concatenating lists

Lists can be concatenated with `+` operator. The `extend()` method can be used to append multiple elements at once:

```python
In [1]: lst = ['a', 'b', 'c']

In [2]: lst.extend(['d', 'e'])

In [3]: lst
Out[3]: ['a', 'b', 'c', 'd', 'e']
```

Note that `append` and `extend` are usually faster than `+` because they are modifying the list in place rather than copying the previous list over. This is similar to R. It's the idea that `list = list + a` is going to be slow.

#### Sorting

The `sort()` method can be used to sort a list in place:

```python
In [1]: lst = [1, 3, 2]

In [2]: lst.sort()

In [3]: lst
Out[3]: [1, 2, 3]
```

Note that you can also use the `key` argument in `sort()` to sort the elements by a function that produces a valye to sort the objects.

#### Binary search and maintaining a sorted list

The `bisect` module implements a binary search to insert into a sorted list. `bisect.bisect` identifies the location where an element whould be inserted to keep it sorted, while `bisect.insort` actually inserts the element.

```python
In [1]: import bisect

In [2]: lst = [1, 2, 3, 4, 5, 7]

In [3]: bisect.bisect(lst, 2)
Out[3]: 2

In [4]: bisect.insort(lst, 2)

In [5]: lst
Out[5]: [1, 2, 2, 3, 4, 5, 7]
```

#### Slicing

Most sequence types can be subsetted using "slicing" notation. For example:

```python
In [1]: lst = ['a', 'b', 'c', 'd', 'e']

In [2]: lst[2:3]
Out[3]: ['c', 'd']
```

Note that while the first element of the slice notation in included, the second is excluded. This is different than R. If one of the numbers is omitted, the first element or last element of the sequence is then included. Negative indices slice the sequence relative to the end of the sequence.
