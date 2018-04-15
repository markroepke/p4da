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

Note that `append` and `extend` are usually faster than `+` because they are modifying the list in place rather than copying the previous list over. This is similar to R. It is the idea that `list = list + a` is going to be slow.

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

### Built-in sequence functions

#### enumerate

When iterating over a sequence, it is useful to know the index of the sorted column. This could be done with:

```python
i = 0
for value in sequence:
    i = i + 1             # note that `i += 1` is equivalent here
    print('Current index is ' + str(i))
```

But because this is so common, you can also do:

```python
for i, value in enumerate(sequence):
    print('Current index is ' + str(i))
```

#### sorted

The `sorted()` function can be used to return a sorted list from the elements of any sequence:

```python
In [1]: sorted([2, 4, 3, 5])
Out[1]: [2, 3, 4, 5]
```

#### zip

The `zip()` function pairs up multiple sequences to create a list of tuples:

```python
In [1]: seq_1 = ['foo', 'bar', 'zoo']

In [2]: seq_2 = [1, 2, 3]

In [3]: zip(seq_1, seq_2)
Out[3]: [('foo', 1), ('bar', 2), ('zoo', 3)]
```

#### reversed

`reversed` is a *generator* that iterates over the elements in a sequence in reverse order (note that this doesn't happen until it's used in a `for` loop or the `list()` function:

```python
In [1]: list(reversed(range(2)))
Out[1]: [2, 1, 0]
```

### dict

`dict` is the most important built-in data structure. Within programming, it is more commonly known as a *hash map* or *associative array*. A `dict` is flexible-in-size, meaning it can be mutated, collection of key-value pairs. A common way of creating a `dict` is the use of curly braces and colons.

```python
In [1]: dict_1 = {'a' : 'apple', 'b' : 'banana', 'c' = 'clementine'}
```

Note that the value of each key-value pair does not need to be of the same type:

```python
In [1]: dict_2 = {'a' : 'apple', 'b' = [1, 2, 3, 4]}
```

Many of the same functionality from `lists` and `tuples` is available for `dicts`:

```python
In [1]: dict_1['d'] = 'doritos'

In [2]: dict_1
Out[2]: {'a' : 'apple', 'b' : 'banana', 'c' = 'clementine', 'd' = 'doritos'}

In [3]: dict_1['b']
Out[3]: 'banana'
```

You can check if a `dict` contains a key by using the `in` operator:

```python
In [1]: 'b' in dict_1
Out[1]: True
```

You can delete values by either using `del` or `pop`.

```python
In [1]: del dict_1['b']

In [2]: dict_1.pop['a']
```

The `keys` and `values` methods gives iterators of the `dict` keys and values:

```python
In [1]: list(dict_1.keys())
Out[1]: ['a', 'b', 'c']

In [2]: list(dict_1.values())
Out[2]: ['apple', 'banana', 'clementine']
```

`dicts` can be merged into one another using the `update` method:

```python
In [1]: dict_1.update({'e' : 'eggplant', 'f' = 'fritos'})
```

#### Creating dicts from sequences

A `dict` is a collection of *key-value* pairs where `key` and `value` are essentially tuples. So the `dict` function can be used to create a `dict` via two `tuples`.

```python
In [1]: dict = dict(zip(range(5), reversed(range(5))))

In [2]: dict
Out[2]: {0: 5, 1: 4, 2: 3, 3: 2, 4: 1, 5: 0}
```
### set

A `set` is an unordered collection of unique elements. `sets` can be created using the `set()` function or via *set literal* with curly braces:

```python
In [1]: set_1 = set([1, 2, 3])

In [2]: set_2 = {1, 2, 3}
```

`sets` support mathematical set operations:

```python
In [1]: a = {1, 2, 3, 4, 5}

In [2]: b = {1, 3, 5, 7, 9}

In [3]: a.union(b)
Out[3]: {1, 2, 3, 4, 5, 7, 9}

In [4]: a.intersection(b)
Out[3]: {1, 3, 5}
```

### List, Set, and Dict Comprehensions

*List comprehensions* are loved by Python users. They allow you to concisely form a new list by filtering the elements of a collection, transforming the elements passing the filter in one concise expression:

```python
[expr for val in collection if condition]
```

This is equivalent to:

```python
result = []
for val in collection:
    if condition:
        result.append(expr)
```

Here is an example:

```python
In [1]: strings = ['a', 'banana', 'c', 'doritos']

In [2]: [x.upper() for x in strings if len(x) > 2]
Out[2]: ['a', 'BANANA', 'c', 'DORITOS']
```

`set` and `dict` comprehensions are a natural extension. Here is a `dict` comprehension:

```python
dict_comp = {key-expr : value-expr for value in collection if condition}
```

And `set` comprehension is:

```python
set_comp = {expr for value in collection if condition}
```

#### Nested list comprehensions

Nested comprehensions can be helpful when working with nested objects:

```python
In [1]: all_data = [['a', 'b', 'c'], ['a', 'b', 'd']]

In [2]: result = [letter for letters in all_data for letter in letters if letter.count('a') >= 1]
```

