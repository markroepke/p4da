# Preliminaries

## 1.1) What Is This Book About?

This book focuses on how Python can be used for data analysis rather than how to do data analysis. Methodologies will not be covered, while specific data-oriented Python packages will be covered. This is likely ideal for me.

### What Kinds of Data?

The primary focus will be on structured data. This includes:

* tabular data
* multidimensional arrays (matrices)
* relational data
* time series

## 1.2) Why Python for Data Analysis?

Python has been a language-of-choice for many a variety of people. Its first appearance was in 1991 and has become increasingly popular since 2005. It is an interepreted language known for its versatility, and it has become a premier language for data analysis along with R.

### Python as Glue

Python has the ability to "glue" together many historically important languages like C, C++, and Fortran. This makes it a popular choice for organizations looking to maintain legacy work while also developing new work.

### Solving the "Two-Language" Problem

It is common to research and prototype ideas in R and productionalize those ideas in Java, C#, or C++. There is an argument that Python can be used for research and productionalization, which would be a huge benefit.

### Why Not Python?

Python will usually be slower than Java or C++ because it is interpreted rather than compiled. However, *programmer time* with Python will likely be less and that is usually more valuable.

## 1.3) Essential Python Libraries

### NumPy

NumPy is short for Numerical Python and is a key piece of numerical computing in Python. It provides data structures, algorithms, and glue needed for scientific applications. Specifically:

* A fast and efficient multidimensional array object *ndarray*
* Functions for performing element-wise computations with arrays or mathematical operators between arrays (this is like R)
* Tools for reading and writing array-baseed datasets
* Linear algebra, Fourier transform, and random number generation
* C API to enable Python extensions and C, C++ code to access data structures of NumPy

NumPy arrays are frequently used as a container for numerical data between operations. They are more efficient than the built-in Python data structures, so many numerical computing tools assume the numerical data is in a NumPy data structure like *ndarray*

### pandas

pandas provides data strucutres and functions designed for tabular data, specifically the `DataFrame` and the `Series`. pandas combines the strengths of NumPy (high-performance, array-computing) with the data transformation and manipulation capabilities of something like SQL. pandas is a primary focuse of this book because of the importance of preparing data for data analysis.

For R users, the `DataFrame` is similar to the `data.frame` object in R. 

The name "pandas" is derived from the *panel data* and a play on *Python data analysis*.

### matplotlib

matplotlib is the most popular Python library for producing two-dimensional data visualizations. It is designed to create plots suitable for publication. There are other visualization libraries available, but matplotlib is the most widely used and is a good choice as a default visualization tool.

### IPython and Jupyter

IPython began in 2001 to provide and interactive framework to Python computing. This is an important feature for data analysis, as data work frequently requires one to execute and explore results interactively. IPython became Jupyter, which is language-agnostic. Jupyter also supports Markdown and renders in HTML for communication.

### SciPy

SciPy is a collection of packages addressing standard problems in scientific computing, including differential equation solvers, linear algebra, optimizers, sparse matrices, statistics. When combined with NumPy, many scientific computing tasks can be achieved in with SciPy.

### scikit-learn

scikit-learn is the premier machine learning toolkil for Python. It includes submodules for classification, regression, clustering, dimension reduction, model selection, and preprocessing. scikit-learn has helped make Python a language-of-choice for many data scientists.

### statsmodels

statsmodels was inspired by the frequentist statistical and econometric models available in R. It is more focused on statistical inference rather than prediction.

## 1.4) Installation and Setup

I am running Ubuntu over Windows 10 so I have elected to follow the Linux installation instructions. I have installed Python 3.6.4 through the Anaconda distribution.

### Installing or Updating Python Packages

The command `conda install *package_name*` can be used to install Python packages. The command `conda update *package_name*` can be used to update Python packages. 

### Python 2 and Python 3

Python was introduced in 1991 and many lessons had been learned over the time. In result, a "breaking" release of Python 3 occured at the end of 2008. For a while, the Python data community continued to use Python 2.7 because not all libraries were compatible with Python 3. However, that is not the case anymore and data analysis should be done in Python 3 because Python 2 will lose support in 2020.

### IDEs and Text Editors

The IPython shell can be very helpful. However, there are IDEs available: PyDev, PyCharm, Python Tools for Visual Studio, Spyder, Komodo.

## 1.5) Community and Conferences

### Communities

pydata is a Google Group list for questions related to Python for data analysis.

### Conferences

PyData is a worldwide series of regional conferences targeted at dat science and data analysis use cases

## 1.6) Navigating This Book

Chapters 2 and 3 are good for those with little experience in Python -- I consider myself in that group. Then, an brief overview of NumPy, and introduction to Pandas. 

Topics fall into different categories that resemble the data science workflow:

* Interacting with the outside world
* Preparation
* Transformation
* Modeling and computation
* Presentation

### Code Examples

Code examples appear as they would in IPython or Jupyter:

```
In [5]: CODE EXAMPLE
Out[5]: OUTPUT
```

### Data for Examples

Examples datasets can be found on [GitHub](http://github.com/wesm/pydata-book). I will download these using Git.

### Import Conventions

There are common naming conventions for importing modules:

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
import statsmodels as sm
```

Note that it is generally considered bad practice to load entire library like `from numpy import *`.

### Jargon

Munge/wrangle: the overall process of manipulating data into a clean form.
Pseudocode: a description of a process that takes a code-like form while likely not being actual valid source code
Syntactic sugar: programming syntax that does not add new featres, but makes something more convenient or easier to type


