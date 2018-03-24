# Chapter 2: Python Language Basics, IPython, and Jupyter Notebooks

Python and data science have both matured since the first edition of *Python for Data Analysis*, and they have also grown together. Because this book is meant as an introductory text to doing data analysis with Python, a self-contained basic Python overview is necessary. However, it is not imperative to master all parts of Python to be able to do good data analysis in Python. With that being said, the more Python that a person understands, the better. It is encouraged to follow along with IPython and/or Jupyter.

## 2.1) The Python Interpreter

Python is an *interpreted* language rather than a *compiled* language. This means that the Python interpreter executes one line at a time. The standard interpreter can be invoked by running `python` from the command line.

The `>>>` is the *prompt* where the code will be typed. To exit, run `exit()` or CTRL + D.

Running Python program is as simple as calling `python` followed by a `.py` file as its first argument.

The IPython shell is more common for data analysis and scientific computing. In addition, Jupyter is very popylar. You can launch the IPython shell by running the `ipython` command. When the `%run` command is used from within IPython, the `.py` file is executed and its results are available in the IPython session.

Note that the *prompt* in IPython is not `>>>`, but rather `[1]`.

## 2.2) IPython Basics

This section is designed to get up-and-running with IPython shell and Jupyter notebooks.

### Running the IPython Shell

Use the `ipython` command to launch the IPython shell. Arbitrary Python statement can be executed by pressing Enter. Many data objects are formatted for pretty-printing within IPython.

### Running the Jupyter Notebook

Jupyter Notebooks are great for exploratory analysis and communication. To start Jupyter, run `jupyter notebook`. To create a new notebook, click "New" and then "Python 3". The extension for this file is `.ipynb`. These files contain the entire notebook and can be loaded and edited by other Jupyter users. 

### Tab Completion

A major improvement of IPython over the standard Python shell is tab completion. While entering expressions in the shell, pressing the TAB key will search the namespace for any objects or functions matching the characters typed so far. This also works in Jupyter for notebooks. Tab completion also works for methods and attributes as well as modules. Filepaths can also be tab completed and so can function argument names.

### Introspection

Using a question mark before or after a variable will display general info abou the object. This is referred to as *object instrospection*. If the object is a function `?` will also display its docstring, which is similar to help documentation. If you use `??`, the source code of the function will be displayed.

### The %run Command

You can run Python scripts from within IPython using the `%run` command. In addition, command-line arguments can be passed following the file name. Note that the `-i` argument will give the script access to the variables already defined in the environment. This could be helpful for creating an `orchestrator.py` file.

In Jupyter, the `%load` function will import the script text (code) into the code cell.

#### Interrupting running code

CTRL + C will interrupt any running Python code. However, if the Python running calls compiled code then you will either have to wait until control is returned to Python or forcibly terminate the process.

### Executing Code from the Clipboard

The magic function `%cpaste` can be used to paste the copied code into a Jupyter cell.

### Terminal Keyboard Shortcuts

IPython has many keyboard shortcuts that are similar to Emacs. Jupyter has a different set of keyboard shortcuts that are in the integrated help system in the Jupyter menus.

### About Magic Commands

IPython has special commands that are not built into Python itself that are called *magic commands*. All of these *magic commands* are prefixed by the % symbol. An example is the `%timeit` magic command, which times any Python statement:

```python
a = mp.random.randn(100, 100)
%timeit np.dot(a, a)
```

Magic functions can be used by default without the percent sign as long as no variable is defined with the same name as the magic funciton in question. This is called *automagic* and can be enabled/disabled using `%automagic`. 

### Matplotlib Integration

People like IPython because it integrates well with data visualization libraries like matplotlib. The `%matplotlib` magic function is vital in an IPython session to set up the visualization ability in the IPython session. For Jupyter, `%matplotlib inline` should be used.

## 2.3) Python Language Basics

This is an overview of Python language mechanics and concepts. Data structures, functions, and other built-in tools will be covered later.

### Lanugage Semantics

The Python language is considered to be very readable with some calling it "executable pseudocode".

#### Indentation, not braces

Python uses whitespace (tabs or spaces) to structure code rather than braces like R and C++. Consider a for loop:

```python
for x in array:
   if x < 5:
       print("x is less than 5")
   else:
       print("x is not less than 5")
```

The colon denotes the start of an indented code block (what would traditionally be in braces). When the code is no longer indented, it is outside the block. Four spaces is the standard indention for Python.

Similar to R, Python statements do not need to be terminated by semi-colon like SAS or SQL. However, semi-colons can be used to put multiple statements on a single line.

#### Everything is an object

The *object model* of Python is important. Everything in Python is an object and has its own type (function, string, etc.) and internal data. This makes the language very flexible.

#### Comments

Any text can be commented with the hash mark, `#`.

#### Function and object method calls

Functions are called in Python using parentheses and zero or more arguments. You can optionally assign the result to a variable:

```python
result = f(x) 
```

Objects can have funtions attached to them -- these are called *methods*. You can call them like this:

```python
result.some_method(y)
```

Note that functions can take both positional and keyword arguments.

#### Variables and argument passing

This is really important, because it is different than R. In Python, when you assign an object to a variable, you are really just creating a reference to the object.

```python
a = 10
```

We can then copy `a` into `b`:

```python
b = a
```

In R, if we add 4 to `a`, be will remain `10`. That is not the case in Python.

```python
In [1]: a = 10 + 4
In [2]: b
Out[2]: 14
```

Understanding this well is vital when working with larger data sets. Note that assignment is also known as *binding*. 

#### Dynamic references, strong types

Unlike PL/SQL, object references have to specific type associated with them, but are they type of the object they refer to. This is similar to R.
It is because the type is store in the object itself rather than the reference. You can chech to see if an object is of an certain type:

```python
x = 10
isinstance(x, int)
```

#### Attributes and methods

Python objects have attributes and methods. Attributes are Python objects stored inside the object, while methods are functions associated with the object that have access to the internal data of the object. Both can be accessed with `obj.attribute_name()` and can be displayed with `obj.<PRESS TAB>`.

#### Duck typing

Sometimes you want to know if an object has a specific method or behavior -- this is called *duck typing*. 

#### Imports

In Python, a *module* is simply a file with a `.py` extension contain Python code. If we wanted to access the variables and functions from a module, we could run:

```python
import module.py
```

#### Binary operators and comparisons

Most of the mathematical operators are as you might expect. Note that `a ** b` is a^b. To check if two references refer to the same object, use `is`. Comparisons are the same as R. 

#### Mutable and immutable objects

Most objects in Python are mutable, including lists, dicts, NumPy arrays. This means that the object or values that they contain can be modified:

```python
In [1]: a_list = ['foo', 2, [4, 5]]

In [2]: a_list[2] = (3, 4)

In [3]: a_list
Out[3]: ['foo', 2, (3, 4)]
```

Others, like strings and tuples, are immutable.

### Scalar Types

Python has a built-in "single value" types for handling numerical data, strings, booleans, and date and time. Thes values are known as *scalers*. The default scalar types are below:

| Type | Description |
|------|-------------|
| None | The default Python "null" value. There is only one version of this. |
| str  | String type; holds UTF-8 encoded strings |
| bytes | Raw ASCII bytes |
| float | Double-precision floating-point number (note there is no separate "double" type) |
| bool | A `True` or `False` value |
| int | Arbitrary precision signed integer |

#### Numeric types

The primary Python types for numbers are `float` and `int`. Note that `int` can be arbitrarily long and `float` is stored as a 64-bit value and can be expressed with scientific notation:

```python
In [1]: fval = 6.78e-5

In [2]: fval
Out[2]: 6.78e-05
```

Also note that `int` divided by `int` does not always result in an `int`:

```python
In [1]: 3/2
Out[1]: 1.5
```

#### Strings

One of the strings of Python is its powerful string-handling. You can write *string literals* using either single quotes '' or double quotes "". For multiline strings that include breaks, you can use triple quotes (with either single or double):

```python
a = '''
This is a
multiline
quote
'''
b = """
This is also a
multiline
quote
"""
```

Note that both `a` and `b` have five lines of text. We can find this by using the `count` method associated with the objects.

```python
In [1]: a.count("\n")
Out[2]: 4
```

Also, note that strings are *immutable*, meaning they cannot be changed:

```python
In [1]: a = "This is a string."

In [2]: a[10] = "F"
-------------------------------
Type Error

...

```

Many Python objects can be converted into strings using the `str` function:

```python
In [1]: a = 5.6

In [2]: type(a)
Out[2]: float

In [3]: s_a = str(a)

In [4]: type(s_a)
Out[4]: str
```

Strings in Python are simply just sequences of characters so they can be treated like other sequences like `lists` and `tuples`:

```python
In [1]: s = "python"

In [2]: list(s)
Out[2]: ["p", "y", "t", "h", "o", "n"]

In [3]: s[:3]
Out[3]: "pyt"
```

The syntax used above, `[:3]`, is called *slicing*. It is used extensively for sequences and will be explained later.

As with most languages, `\` is the escape character, so you need to use `\\` to write a string literal with a backslash. However, you can always prefix the string literal with `r`, which stands for *raw*, to force the string literal to read all characters as is:

```python
In [1]: r"this\has\no\special\characters"
Out[1]: "this\\has\\no\\special\\characters"
```

Strings can be concatenated simply using `+`:

```python
In [1]: a = "this is the first half"

In [2]: b = " and this is the second half"

In [3]: a + b
Out[3]: "this is the first half and this is the second half"
```

String formatting is an important topic in Python. It allows you to format a string template and pass arguments to one of its `format` method. For example:

```python
In [1]: template = "{0:.2f} {1:s} are worth ${2:d}"
```

In this template:

* {0:.2f} means to format the first argument (0) as a `float` (f) with two decimal places
* {1:s} means to format the second argument (1) as a `str` (s)
* {2:d} means to format the third argument (2) as an `int` (d)

And we can then use the `format` method on `template` to evaluate it:

```python
In [2]: template.format(4.5560, "Argentine Pesos", 1)
Out[2]: "4.56 Argentine Pesos are worth $1"
```

#### Bytes and Unicode

In Python 3.0+, you can convert string literals into UTF-8 encoding when dealing with non-ASCII text:

```python
In [1]: s = "español"

In [2]: s.encode('utf-8')
Out[2]: b'espa\xc3\xb1ol'
```

#### Booleans

The two boolean values are written as `True` and `False` in Python, and can be combined with the `and` and `or` keywords.

#### Type casting

Similar to `str` and `str()`, there are functions that can be used to cast values to other types like `bool`, `int`, and `float`:

```python
In [1]: s = "3.14159"

In [2]: fval = float(s)

In [3]: type(fval)
Out[3]: float
```

#### None

`None` is the Python "null" value. It is often used as a default function argument and can be combined with the `is` keyword.

#### Dates and times

The built-in `datetime` module is helpful when dealing with `date`, `time`, or `datetime` types. It can be loaded with:

```python
from datetime import date, time, datetime
```

`datetime` objects have helpful methods like `date` and `time` that can extract the `date` or `time` from the `datetime` object. This is helpful for conversion. In addition, `strftime` formats a `datetime` as a `str`.

`datetime` type is immutable.

The difference between two `datetime` objects will create a `datetime.timedelta` type.

### Control Flow

#### if, elif, and else

The `if` statement:

```python
if x < 0:
    print(str(x) + ' is less than zero')
```

`elif` and `else`:

```python
if x < 0:
    print(str(x) + ' is less than zero')
elif x > 0:
    print(str(x) + ' is greater than zero')
else:
    print(str(x) + ' is equal to zero')
```

Once a condition evaluate to `True`, none of the following `if`, `elif`, or `else` blocks will be reached -- the block will be exited.

#### for loops

Standard syntax for `for` loops:

```python
for value in collection:
    # do something with value
```

You can skip to the next iteration with the `continue` keyword:

```python
for i in [1, 2, 3, 4, 5]:
    if i % 2 == 0:
        continue
    print(str(i) + ' is an odd number')
```

And a `for` loop can be exited with the `break` keyword.

#### while loops

Example of a `while` loop:

```python
x = 256
total = 0
while x > 0:
    if total > 500:
        break
    total += x
    x = x//2
```

#### pass

In R, whitespace can be used as "nothing", but in Python whitespace is used to delimit blocks. Therefore, the `pass` statement must be used to represent "no operation":

```python
if x > 0:
   print("Positive!")
elif x < 0:
   pass
else:
   print("Zero!")
```

#### range

The `range` function is similar to the `seq()` function in R:

```python
for i in range(9, -1, -1):
    print(str(i) + " bottles of beer on the wall.")
```

Note that the end number is not included in the range! This is different than `seq()`.

#### Ternary expressions

You can combine `if-else` blocks into a single line with a *ternary expression*:

```python
value = "non-negative" if x >= 0 else "negative"
```

This is clean but sacrifices readability.





