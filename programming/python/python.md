# Table of Contents
- [Table of Contents](#table-of-contents)
  - [python basics](#python-basics)
    - [PEP 8](#pep-8)
    - [PYTHONPATH](#pythonpath)
    - [pyc files](#pyc-files)
    - [flake8 and black](#flake8-and-black)
    - [setup.py](#setuppy)
    - [virtualenv](#virtualenv)
    - [module vs package](#module-vs-package)
    - [namespace](#namespace)
    - [memory management](#memory-management)
    - [built-in data types](#built-in-data-types)
    - [split function](#split-function)
    - [regex](#regex)
    - [exception handling](#exception-handling)
    - [context manager](#context-manager)
    - [args and kwargs](#args-and-kwargs)
    - [dataclass](#dataclass)
    - [shallow and deep copy](#shallow-and-deep-copy)
  - [functions and functional features](#functions-and-functional-features)
    - [closure](#closure)
    - [global local and nonlocal](#global-local-and-nonlocal)
    - [first-class and higher-order functions](#first-class-and-higher-order-functions)
    - [dunder/magic/special methods](#dundermagicspecial-methods)
    - [lambda function](#lambda-function)
    - [decorator](#decorator)
    - [generator](#generator)
    - [map function](#map-function)
    - [filter function](#filter-function)
    - [reduce function](#reduce-function)
  - [collections and data structures](#collections-and-data-structures)
    - [slicing](#slicing)
    - [comprehensions](#comprehensions)
    - [different ways to fetch item](#different-ways-to-fetch-item)
    - [dictionaries merge and update](#dictionaries-merge-and-update)
    - [list vs tuple](#list-vs-tuple)
    - [array vs list](#array-vs-list)
  - [object-oriented programming](#object-oriented-programming)
    - [class](#class)
    - [object](#object)
    - [self keyword](#self-keyword)
    - [super function](#super-function)
    - [operator overriding](#operator-overriding)
    - [prevent method overriding](#prevent-method-overriding)
    - [property decorator](#property-decorator)
    - [meta class](#meta-class)
    - [object creation process](#object-creation-process)
    - [encapsulation](#encapsulation)
    - [inheritance](#inheritance)
    - [polymorphism](#polymorphism)
    - [abstraction](#abstraction)
    - [class diagram](#class-diagram)
    - [method resolution order](#method-resolution-order)
    - [inheritance vs composition](#inheritance-vs-composition)
    - [staticmethod vs classmethod](#staticmethod-vs-classmethod)
    - [class variable vs instance variable](#class-variable-vs-instance-variable)
    - [mutable default parameter](#mutable-default-parameter)
    - [monkey patching](#monkey-patching)
    - [type hinting](#type-hinting)
  - [async and concurrency](#async-and-concurrency)
    - [thread vs process](#thread-vs-process)
    - [cpu-bound vs i/o-bound tasks](#cpu-bound-vs-io-bound-tasks)
    - [global interpreter lock](#global-interpreter-lock)
    - [race condition](#race-condition)
    - [asyncio](#asyncio)
    - [async context manager](#async-context-manager)
    - [future object](#future-object)
  - [References](#references)

##  python basics

### PEP 8

Python Enhancement Proposal or `PEP 8` is a set of rules that specify how to format Python code for maximum readability.

--- 

### PYTHONPATH

`PYTHONPATH` is a special environment variable that provides guidance to the Python interpreter about where to find various libraries and applications.

---

### pyc files

When you write a Python program and run it, the Python interpreter first compiles the source code into bytecodes and then executes the bytecodes to produce the desired output.

But when you go to make the soda, you don't actually follow the recipe in English. You translate it into a series of instructions that your soda machine can understand – these instructions are the "bytecodes".

In Python, bytecodes are a lower-level representation of the source code of a Python program.

They are typically stored in files with an `.pyc` extension, which stands for "Python compiled code". These files are created automatically by the Python interpreter when it encounters a `.py` file that it needs to execute.

They are used to speed up the execution of Python programs by avoiding the need to recompile the source code each time the program is run.

---

### flake8 and black

`Flake8` is a linter tool that checks your code for style and syntax errors, while `Black` is a code formatter that automatically formats your code according to a set of predefined rules. By using `Flake8` and `Black`, you can ensure the good quality of your Python code.

```shell
# flake8
pip install flake8
flake8 .


# black
pip install black
black .
```

---

### setup.py

In Python, setup.py is a module used to build and distribute Python packages. It typically contains information about the package, such as its name, version, and dependencies, as well as instructions for building and installing the package.

```python

from setuptools import setup

setup(
    name='my_package',
    version='0.1',
    description='A sample Python package',
    author='John Doe',
    author_email='jdoe@example.com',
    packages=['my_package'],
    install_requires=[
        'numpy',
        'pandas',
    ],
)
```

```shell
pip install setuptools 
python setup.py sdist bdist_wheel 
pip install my_package 
```

---

### virtualenv

In a nutshell, Python virtual environments help decouple and isolate Python installs and associated pip packages. This allows end-users to install and manage their own set of packages that are independent of those provided by the system or used by other projects.

- *Install it:*
``` shell
$ python3 -m venv venv
```
- *Activate it:*
``` shell
$ source venv/bin/activate
```
- *Install Packages Into It:*
``` shell
(venv) $ python -m pip install <package-name>
```

---

### module vs package

- *Module:*
The module is a Python file that contains collections of functions and global variables and with having a .py extension file.

- *Package:*
The package is a directory having collections of modules. This directory contains Python modules and also having `__init.py__` file by which the interpreter interprets it as a Package.

---

### namespace

A naming system used to make sure that names are unique to avoid naming conflicts refers to as Namespace.

---

### memory management

Unlike other programming languages, python stores references to an object after it is created. For example, an `[]` object might have two references a and b. The memory manager in python keeps track of the reference count of each object, this would be 2 for `[]` object. Once the object reference count reaches 0, object is removed from memory.

The reference count:
- increases if an object is assigned a new name or is placed in a container, like tuple or dictionary.
- decreases when the object's reference goes out of scope or when name is assigned to another object. Python's garbage collector handles the job of removing objects & a programmer need not to worry about allocating/de-allocating memory like it is done in C.

```python
import sys

def main():
    """
    >>> a = []
    >>> sys.getrefcount(a)
    2
    >>> b = a
    >>> a is b
    True
    >>> sys.getrefcount(a)
    3
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### built-in data types

| Data Types |           Classes            |                       Description |
| ---------- | :--------------------------: | --------------------------------: |
| Numeric    |     int, float, complex      |              holds numeric values |
| String     |             str              |      holds sequence of characters |
| Sequence   |      list, tuple, range      |         holds collection of items |
| Mapping    |             dict             | holds data in key-value pair form |
| Boolean    |             bool             |    holds either `True` or `False` |
| Set        |       set, frozeenset        |   hold collection of unique items |
| Binary     | bytes, bytearray, memoryview |       hold collection binary data |

- Tuples and strings are the only fundamental collection in Python which is immutable.
- Lists, sets, dictionaries are all mutable.
- Integers, floats, and booleans are all immutable.

Most things are mutable in Python. If you want to keep one of your classes immutable, don't add any methods that change the object's properties.

---

### split function

The split function breaks the string into shorter strings using the defined separator. It returns the list of all the words present in the string.

```python
cars = 'BMW-Tesla-Range Rover'


def main():
    """
    >>> print(cars.split('-'))
    ['BMW', 'Tesla', 'Range Rover']
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### regex

A **Reg**ular **Ex**pression (RegEx) is a sequence of characters that defines a search pattern.

```python
import re

line1 = "Should we use regex more often? Let me know at doggy@poop.com"
match1 = re.search(r'[\w.+-]+@[\w-]+\.[\w.-]+', line1)

line2 = f'{line1} or doggy.support@poop.com'
match2 = re.findall(r'[\w.+-]+@[\w-]+\.[\w.-]+', line2)


def main():
    """
    >>> match1.group(0)
    'doggy@poop.com'
    >>> match2
    ['doggy@poop.com', 'doggy.support@poop.com']
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
---

### exception handling

Exception handling is the way by which a programmer can control an error within the program without breaking out the flow of execution.

```python
class SatanError(Exception):
    pass


def fraction(num):
    try:
        if num == 666:
            raise SatanError
        1 / num
    except (ZeroDivisionError, SatanError) as ex:
        print(ex.__class__.__name__)
    except Exception as ex:
        print(ex.__class__.__name__)
    else:
        print('else')
    finally:
        print('finally')


def main():
    """
    >>> fraction(666)
    SatanError
    finally
    >>> fraction(0)
    ZeroDivisionError
    finally
    >>> fraction('ten')
    TypeError
    finally
    >>> fraction(3)
    else
    finally
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

*Examples* : `TypeError`, `ValueError`, `ImportError`, `KeyError`, `IndexError`, `NameError`, `PermissionError`, `EOFError`, `ZeroDivisionError`, `StopIteration`

---

### context manager

The `with` statement simplifies exception handling by encapsulating common preparation and cleanup tasks in so-called context managers.

For instance, the `open` statement is a context manager in itself, which lets you open a file, keep it open as long as the execution is in the context of the `with` statement where you used it, and close it as soon as you leave the context, no matter whether you have left it because of an exception or during regular control flow.

:memo: *File CRUD:*

```python
from os import remove
from os.path import isfile

file_name = 'temp.txt'


def write(file, num=4):
    with open(file, 'w') as file:
        file.writelines([f'{n**2};' for n in range(num)])


def read(file):
    with open(file, 'r') as file:
        return file.read()


def update(file):
    with open(file, 'r+') as file:
        data = file.read()
        file.write(data[::-1])


def delete(file):
    if isfile(file):
        remove(file)


def main():
    """
    >>> file_name = 'temp.txt'
    >>> write(file_name)
    >>> read(file_name)
    '0;1;4;9;'
    >>> update(file_name)
    >>> read(file_name)
    '0;1;4;9;;9;4;1;0'
    >>> delete(file_name)
    >>> isfile(file_name)
    False
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:memo: *Custom ContextManager*

Context managers need a `__enter__` method and a `__exit__` method, and the `__exit__` method should accept three positional arguments. The `as` keyword will point a given variable name to the return value from the `__enter__` method.


```python
import time

class Timer:
    def __enter__(self):
        self.start = time.perf_counter()
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.stop = time.perf_counter()
        self.elapsed = self.stop - self.start

def main():
    """
    >>> with Timer() as t:
    ...     result = sum(range(10_000_000))
    >>> t.elapsed > 0
    True
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:memo: It is also possible to write a context manager using generator syntax thanks to the `contextlib.contextmanager` decorator

```python
from contextlib import contextmanager


@contextmanager
def context_manager(num):
    print('Enter')
    yield num + 1
    print('Exit')


def main():
    """
    >>> with context_manager(2) as cm:
    ...     print(cm)
    Enter
    3
    Exit
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### args and kwargs

- Use `*args` when we aren't sure how many arguments are going to be passed to a function, or if we want to pass a stored list or tuple of arguments to a function.

- `**kwargs` is used when we don't know how many keyword arguments will be passed to a function, or it can be used to pass the values of a dictionary as keyword arguments.  

```python
from functools import reduce


def multiply(*args):
    assert args.__class__.__name__ == 'tuple'
    return reduce(lambda a, b: a * b, args)


def url_formatter(**kwargs):
    assert kwargs.__class__.__name__ == 'dict'

    protocol = kwargs.get('protocol', 'http')
    server = kwargs.get('server', '127.0.0.1')
    port = kwargs.get('port', 8080)
    endpoint = kwargs.get('endpoint', 'index.html')

    return f'{protocol}://{server}:{port}/{endpoint}'


config = {
    'protocol': 'https',
    'endpoint': 'api/docs',
}

url_formatter(**config)


def main():
    """
    >>> multiply(4, 5)
    20
    >>> multiply(2, 2, 2)
    8
    >>> url_formatter(server='localhost', port=80)
    'http://localhost:80/index.html'
    >>> url_formatter(**config)
    'https://127.0.0.1:8080/api/docs'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

```python
def ordering(arg_1, arg_2, *args, kw_1="shark", kw_2="blobfish", **kwargs):
    pass
```

---

### dataclass

`Dataclasses` are python classes, but are suited for storing data objects. This module provides a decorator and functions for automatically adding generated special methods such as `__init__()` and `__repr__()` to user-defined classes.

```python
from dataclasses import dataclass, field


@dataclass(frozen=True)
class Position:
    name: str = 'Kyiv'
    lon: float = 30.31
    lat: float = 50.27

    def __repr__(self):
        return f"name={self.name};lon={self.lon};lat={self.lat};"


@dataclass(frozen=True)
class Capital(Position):
    country: str = 'Ukraine'
    time_zones: list[str] = field(default_factory=['UTC+2', 'UTC+3'])

    def __repr__(self):
        return f"{super().__repr__()};country={self.country};time_zones={self.time_zones};"


def main():
    """
    >>> capital = Capital('Oslo', 10.44, 59.54, 'Norway', ['UTC+1', 'UTC+2'])
    >>> print(capital)
    name=Oslo;lon=10.44;lat=59.54;;country=Norway;time_zones=['UTC+1', 'UTC+2'];
    >>> capital.name = 'Bergen'
    Traceback (most recent call last):
    ...
    dataclasses.FrozenInstanceError: cannot assign to field 'name'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)

```

---

### shallow and deep copy

:bulb: The difference between shallow and deep copying is only relevant for compound objects (objects that contain other objects, like lists or class instances):

  - A shallow copy constructs a new compound object and then (to the extent possible) inserts references into it to the objects found in the original.

  - A deep copy constructs a new compound object and then, recursively, inserts copies into it of the objects found in the original.

```python
import copy

a = [1, 2, 3]
b = [4, 5, 6]
c = [a, b]


def main():
    """
    >>> # using assignment operator to copy
    >>> d = c
    >>> id(c) == id(d)          # d is the same object as c
    True
    >>> id(c[0]) == id(d[0])    # d[0] is the same object as c[0]
    True

    >>> # using a shallow copy
    >>> d = copy.copy(c)
    >>> id(c) == id(d)          # d is now a new object
    False
    >>> id(c[0]) == id(d[0])    # d[0] is the same object as c[0]
    True

    >>> # using a deep copy
    >>> d = copy.deepcopy(c)
    >>> id(c) == id(d)          # d is now a new object
    False
    >>> id(c[0]) == id(d[0])    # d[0] is now a new object
    False
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
---

##  functions and functional features

### closure

Python closure is a nested function that allows us to access variables of the outer function even after the outer function is closed.

```python
def greet():
    name = "John"
    return lambda: "Hi " + name


def main():
    """
    >>> greet()()
    'Hi John'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### global local and nonlocal


:bulb: *global*

In Python, the `global` keyword allows us to modify the variable outside of the current scope. 
It is used to create a global variable and make changes to the variable in a local context.

```python 
foo = 0  # <- 〇


def outer():
    foo = 5  # <- ✖

    def middle():
        foo = 10  # <- ✖

        def inner():
            global foo  # Here
            foo += 1
            print(foo)  # 1
        inner()
    middle()


def main():
    """
    >>> outer()
    1
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:bulb: *nonlocal*

The `nonlocal` statement causes the listed identifiers to refer to previously bound variables in the nearest enclosing scope. This is important because the default behavior for binding is to search the local namespace first. The statement allows encapsulated code to rebind variables outside of the local scope besides the global (module) scope.

```python
foo = 0  # <- ✖


def outer():
    foo = 5  # <- ✖

    def middle():
        foo = 10  # <- 〇

        def inner():
            nonlocal foo  # Here
            foo += 1
            print(foo)  # 11
        inner()
    middle()


def main():
    """
    >>> outer()
    11
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### first-class and higher-order functions

- In Python, the term `first-class function` refers to a function’s ability to be treated as an object that can be assigned to a variable, used as an argument for other functions, and returned as a value. As a result, functions in Python are identical to other objects like `strings`, `integers`, and `lists`.

- `Higher-order functions` are those that accept arguments from other functions or return values that are themselves other functions. The idea of `first-class functions` in Python makes `higher-order functions` possible.

```python
def square(x):  # first-order function
    return x ** 2


def apply_func(func, lst):  # high-order function
    return [func(x) for x in lst]


def make_adder(n):  # high-order function
    def adder(x):
        return x + n
    return adder


def main():
    """
    >>> my_func = square
    >>> my_func(3)
    9
    >>> numbers = [1, 2, 3, 4, 5]
    >>> apply_func(square, numbers)
    [1, 4, 9, 16, 25]
    >>> make_adder(5)(10)
    15
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### dunder/magic/special methods

Dunder (**Double Underscores**) methods are special/magic predefined methods in Python, with names that start and end with a double underscore. They are defined by built-in classes in Python.

```python
def main():
    """
    >>> dir(int)[:4]
    ['__abs__', '__add__', '__and__', '__bool__']
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### lambda function

An anonymous function is known as a lambda function. This function can have only one statement but can have any number of parameters.

```python
greet_user = lambda name : print('Hey there,', name)


def main():
    """
    >>> greet_user('Delilah')
    Hey there, Delilah
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

---

### decorator

A decorator is a design pattern in Python that allows a user to add new functionality to an existing object without modifying its structure.

:bulb: *Simple decorator*

```python
def make_pretty(func):
    def inner():
        print("I got decorated")
        func()
    return inner


def ordinary():
    print("I am ordinary")


decorated_func = make_pretty(ordinary)


def main():
    """
    >>> decorated_func()
    I got decorated
    I am ordinary
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

:bulb: *Decorating functions with parameters*

```python
def smart_divide(func):
    def inner(a, b):
        print("I am going to divide", a, "and", b)
        if b == 0:
            print("Whoops! cannot divide")
            return
        return func(a, b)
    return inner


@smart_divide
def divide(a, b):
    print(a/b)


def main():
    """
    >>> divide(2,5)
    I am going to divide 2 and 5
    0.4

    >>> divide(2,0)
    I am going to divide 2 and 0
    Whoops! cannot divide
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

:bulb: *Chaining decorators in Python*

```python
def star(func):
    def inner(*args, **kwargs):
        print("*" * 15)
        func(*args, **kwargs)
        print("*" * 15)
    return inner


def percent(func):
    def inner(*args, **kwargs):
        print("%" * 15)
        func(*args, **kwargs)
        print("%" * 15)
    return inner


@star
@percent
def printer(msg):
    print(msg)


def main():
    """
    >>> printer("Hello")
    ***************
    %%%%%%%%%%%%%%%
    Hello
    %%%%%%%%%%%%%%%
    ***************
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
:bulb: *Decorators with parameters*

```python
user = {"username": "Anna", "access_level": "user"}


def make_secure(access_level):
    def decorator(func):
        def secure_function(*args, **kwargs):
            if user["access_level"] == access_level:
                return func(*args, **kwargs)
            else:
                return f"No {access_level} permissions for {user['username']}."

        return secure_function

    return decorator


@make_secure('admin')
def get_root():
    return "root:root"


def main():
    """
    >>> get_root()
    'No admin permissions for Anna.'
    >>> user |= {"access_level": "admin"}
    >>> get_root()
    'root:root'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### generator

In Python, a generator is a function that returns an iterator that produces a sequence of values when iterated over.

```python
def fibonacci():
    x, y = 0, 1
    while True:
        yield x
        x, y = y, x + y


def main():
    """
    >>> gen = fibonacci()
    >>> next(gen)
    0
    >>> next(gen)
    1
    >>> next(gen)
    1
    >>> next(gen)
    2
    >>> # generator expression
    >>> squares_generator = (i * i for i in range(4))
    >>> for i in squares_generator:
    ...     print(i)
    0
    1
    4
    9
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### map function

The `map()` function applies a given function to each element of an iterable (`list`, `tuple` etc.) and returns an iterator containing the results.

```python
num1, num2 = [4, 5, 6], [5, 6, 7]

result = map(lambda n1, n2: n1+n2, num1, num2)


def main():
    """
    >>> print(list(result))
    [9, 11, 13]
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

---

### filter function

The `filter()` function selects elements from an iterable (`list`, `tuple` etc.) based on the output of a function.
The function is applied to each element of the iterable and if it returns True, the element is selected by the `filter()` function.

```python
numbers = [1, 2, 3, 4, 5, 6, 7]

even_numbers_iterator = filter(lambda x: (x % 2 == 0), numbers)


def main():
    """
    >>> list(even_numbers_iterator)
    [2, 4, 6]
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()


```

---

### reduce function

Python's `reduce()` function applies a pre-defined function to each element of an iterable (such as a list, tuple, dictionary, etc.) and generates a single-valued result.

```python
def main():
    """
    >>> from functools import reduce
    >>> nums = [1, 2, 3, 4]
    >>> reduce(lambda x, y: x + y, nums)
    10
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

##  collections and data structures

### slicing

Slicing refers to the mechanism to select the range of items from sequence types like lists, tuples, strings

```python
py_string = 'Python'
py_list = ['P', 'y', 't', 'h', 'o', 'n']
py_tuple = ('P', 'y', 't', 'h', 'o', 'n')


def main():
    """
    >>> # stop = 3
    >>> py_string[slice(3)] 
    'Pyt'
    >>> # stop = 3
    >>> py_string[:3]
    'Pyt'
    >>> # start = 1, stop = 6, step = 2
    >>> py_string[slice(1, 6, 2)] 
    'yhn'
    >>> py_list[slice(-1, -4, -1)]
    ['n', 'o', 'h']
    >>> py_tuple[slice(-1, -5, -2)]
    ('n', 'h')
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### comprehensions

List comprehension in Python is a concise way of creating lists from the ones that already exist. It provides a shorter syntax to create new lists from existing lists and their values. 

```python
def main():
    """
    >>> [ x for x in range(20) if x % 2 == 0]
    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
    >>> [y for y in range(100) if y % 2 == 0 if y % 5 == 0]
    [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]
    >>> ["Even" if i % 2 == 0 else "Odd" for i in range(6)]
    ['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']
    >>> matrix = [[1, 2], [3,4], [5,6], [7,8]]
    >>> [[row[i] for row in matrix] for i in range(2)]
    [[1, 3, 5, 7], [2, 4, 6, 8]]
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:bulb: *Dictionary comprehensions*

```python
def main():
    """
    >>> {str(num): num*num for num in range(1, 6)}
    {'1': 1, '2': 4, '3': 9, '4': 16, '5': 25}
    >>> persons = {'Jack': 38, 'Michael': 48, 'Guido': 57, 'John': 33}
    >>> {k: v for (k, v) in persons.items() if v % 2 != 0 if v < 40}
    {'John': 33}
    >>> {k1: {k2: k1 * k2 for k2 in range(1, 4)} for k1 in range(2, 4)}
    {2: {1: 2, 2: 4, 3: 6}, 3: {1: 3, 2: 6, 3: 9}
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```


:bulb: *Set comprehensions*

```python
def main():
    """
    >>> # primes
    >>> {x for x in range(2, 30) if all(x % y for y in range(2, min(x, 11)))}
    {2, 3, 5, 7, 11, 13, 17, 19, 23, 29}
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:bulb: *Generator comprehensions*

There are no tuple comprehensions, but the generator expression might 
be converted to a tuple if it's required.


```python
def main():
    """
    >>> evens = ( number for number in range(1,11) if number % 2 == 0 )
    >>> type(evens).__name__
    'generator'
    >>> next(evens)
    2
    >>> next(evens)
    4
    >>> tuple(evens)   
    (6, 8, 10)
    >>> list(evens)
    []
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```
---

### different ways to fetch item

```python
example_list = [0,1,2,3,4,5,6]


def main():
    """
    >>> # index jump
    >>> example_list[::3]
    [0, 3, 6]
    >>> # list comprehension
    >>> [x for x in example_list if example_list.index(x) % 3 == 0]
    [0, 3, 6]
    >>> i, res = 0, []
    >>> for idx, i in enumerate(example_list):
    ...     if idx % 3 == 0:
    ...         res.append(i)
    >>> res
    [0, 3, 6]
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

---

### dictionaries merge and update

```python
x = {"key1": "value1 from x", "key2": "value2 from x"}
y = {"key2": "value2 from y", "key3": "value3 from y"}


def main():
    """
    >>> # dict merge
    >>> {**x, **y}
    {'key1': 'value1 from x', 'key2': 'value2 from y', 'key3': 'value3 from y'}
    >>> # python3.9
    >>> x | y
    {'key1': 'value1 from x', 'key2': 'value2 from y', 'key3': 'value3 from y'}
    >>> # dict update
    >>> x |= y
    >>> x
    {'key1': 'value1 from x', 'key2': 'value2 from y', 'key3': 'value3 from y'}
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### list vs tuple

1. The literal syntax of tuples is shown by parentheses `()` whereas the literal syntax of lists is shown by square brackets `[]` .
2. Lists has variable length, tuple has fixed length.
3. List has mutable nature, tuple has immutable nature.
4. List has more functionality than the tuple.

- *Mutable List vs Immutable Tuples:*

List has mutable nature i.e., list can be changed or modified after its creation according to needs whereas tuple has immutable nature i.e., tuple can’t be changed or modified after its creation.

```python
list_num = [1, 2, 3, 4]
tup_num = (1, 2, 3, 4)


def main():
    """
    >>> list_num[2] = 5
    >>> print(list_num)
    [1, 2, 5, 4]
    >>> tup_num[2] = 5
    Traceback (most recent call last):
    ...
    TypeError: 'tuple' object does not support item assignment
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)

```

- *Size Comparison:*

Tuples operation has smaller size than that of list, which makes it a bit faster but not that much to mention about until you have a huge number of elements.

```python
a = (1, 2, 3, 4, 5, 6, 7, 8, 9, 0)
b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]


def main():
    """
    >>> print('a =', a.__sizeof__())
    a = 104
    >>> print('b =', b.__sizeof__())
    b = 120
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
---

### array vs list


|                       List                        |                             Array                              |
| :-----------------------------------------------: | :------------------------------------------------------------: |
|   Can contain elements of different data types    |     Contains homogeneous elements only i.e. same data type     |
|                 No need to import                 |               Need to import via numpy or array                |
|    Preferred for short sequence of data items     | Preferred for large sequence of data items i.e., data analysis |
| Can't perform arithmetic operations on whole list |                Great for arithmetic operations                 |

---

##  object-oriented programming

### class

A class in Python is like a blueprint for creating objects. A class defines properties and methods that are common to all objects created from it. 

In Python, you use the `class` keyword to define a class. 

Classes help organize code by grouping related attributes and functions, promoting reusability and modularity.

---

### object

An object in Python is an instance of a class. You can think of it as a specific realization of the blueprint provided by the class. 

An object contains data in the form of attributes and code in the form of methods. When you create an object, you are essentially creating a variable that has all the properties and behaviors defined in the class.

---

### self keyword

The `self` keyword in Python is used within a class to refer to the instance of the object itself. When you define a method inside a class, the first parameter is usually named `self`. It helps you access the attributes and methods of the class within the current object’s context. 

```python
class MyNum:
    def __init__(self, value):
        self.value = value

    def get_value(self):
        return self.value


def main():
    """
    >>> MyNum('infinity').get_value()
    'infinity'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### super function

Python’s `super()` function is used within a class to call a method from a parent class, often within the context of method overriding. 

```python
class Employee:
    def __init__(self, id, name):
        self.id = id
        self.name = name

    def __repr__(self) -> str:
        return f'id={self.id};name={self.name};'


class Freelance(Employee):
    def __init__(self, id, name, email):
        super().__init__(id, name)
        self.email = email

    def __repr__(self) -> str:
        return super().__repr__() + f'email={self.email}'


def main():
    """
    >>> john = Freelance(1, 'John', 'john@example.com')
    >>> str(john)
    'id=1;name=John;email=john@example.com'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### operator overriding

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

def main():
    """
    >>> v1 = Vector(2, 4)
    >>> v2 = Vector(3, 5)
    >>> v1 + v2
    Vector(5, 9)
    """

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
---

### prevent method overriding

By prefixing the method’s name with a double underscore `__`, you make it private to the class, and it cannot be overridden in a subclass. 

---

### property decorator

In Python, the `@property` decorator allows you to treat a method as a property of the class. By using this, you can create a “getter” method, which enables you to access a class method as though it’s an attribute without needing to write parentheses when you call it. This means you can control how the attribute is accessed without directly exposing it. The `@property` decorator provides a way to implement encapsulation.

```python
class Celsius:
    def __init__(self, temperature=0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32

    @property
    def temperature(self):
        return self._temperature

    @temperature.setter
    def temperature(self, value):
        if value < -273:
            raise ValueError("Temperature below -273 isn't possible")
        self._temperature = value


def main():
    """
    >>> temp = Celsius(36.6)
    >>> temp.temperature
    36.6
    >>> temp.temperature = 40
    >>> temp.temperature
    40
    >>> coldest_thing = Celsius(-300)
    Traceback (most recent call last):
    ...
    ValueError: Temperature below -273 isn't possible
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

---

### meta class

In Python everything is an object, even a class is an object. As a result, a class also must have a type. All classes in Python are of 'type' type. Even the class of 'type' is 'type'. So 'type' is the meta class in Python and to create custom meta class, you would need to inherit from 'type'.

- *Use Case of Meta Class:*

A meta class is the class of a class. A class is an instance of a metaclass. A metaclass is most commonly used as a class-factory. When you create an object by calling the class, Python creates a new class (when it executes the 'class' statement) by calling the metaclass.

```python
def main():
    """
    >>> type(17)
    <class 'int'>
    >>> type(int)
    <class 'type'>
    >>> str.__class__
    <class 'type'>
    >>> type.__class__
    <class 'type'>
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```
- *Meta Class call:*

The metaclass is called with the
- name: name of the class,
- bases: tuple of the parent class (for inheritance, can be empty) and
- attributes: dictionary containing attributes names and values.

```python
def init(self, make):
    self.make = make

# type(name, bases, attrs) 
Car = type('Car', (object,), {'__init__': init, '__repr__': lambda self: self.make,  'wheels': 4})
car = Car('Kia')


def main():
    """
    >>> car
    Kia
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
---

### object creation process

When an object of a class is created or a class is instantiated, the `__new__()` method of class is called. This particular method is responsible for returning a new class object. It can be overriden to implement object creational restrictions on class.

1. The constructor of the class is `__new__()`
2. The initializer of the class is `__init__()`.

Initializer is called right after the constructor, if the constructor has not returned a class object, the initializer call is useless.

**Note**: that the reason `__init__()` could use class object(self) to initialize is because when the code flow reaches `__init__()` the object of the class is already created.

---

### encapsulation

*Encapsulation* is an important concept in object-oriented programming that helps to protect the implementation details of an object. In Python, we can achieve encapsulation by using underscore prefixes to indicate the access level.

```python
class MyClass:

    def __init__(self):
        self._protected_var = 10
        self.__private_var = 20


def main():
    """
    >>> obj = MyClass()
    >>> obj._protected_var
    10
    >>> obj.__private_var
    Traceback (most recent call last):
    ...
    AttributeError: 'MyClass' object has no attribute '__private_var'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

---

### inheritance

*Inheritance* promotes code reuse and allows you to create a hierarchy of classes that share common attributes and methods. It helps in creating clean and organized code by keeping related functionality in one place and promoting the concept of modularity. The base class from which a new class is derived is also known as a parent class, and the new class is known as the child class or subclass.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        return 'om nom nom'


class Dog(Animal):
    def speak(self):
        return 'woof'


class Cat(Animal):
    def speak(self):
        return 'meow'


def main():
    """
    >>> dog = Dog("Husky")
    >>> cat = Cat("Cheshire ")
    >>> dog.eat() == cat.eat()
    True
    >>> dog.speak()
    'woof'
    >>> cat.speak() 
    'meow'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:memo: *Different types of inheritance*

- *Single Inheritance* – A single derived class acquires from on single superclass.
- *Multi-Level Inheritance* – At least 2 different derived classes acquire from two distinct base classes.
- *Hierarchical Inheritance* – A number of child classes acquire from one superclass
- *Multiple Inheritance* – A derived class acquires from several superclasses.

---

### polymorphism

Polymorphism is an important concept in object-oriented programming that allows you to write code that can work with objects of different classes in a uniform way. In Python, polymorphism is achieved by using method overriding or method overloading.

Method overriding is when a subclass provides its own implementation of a method that is already defined in its parent class. This allows the subclass to modify the behavior of the method without changing its name or signature.

Method overloading is when multiple methods have the same name but different parameters. Python does not support method overloading directly, but it can be achieved using default arguments or variable-length arguments.

```python
class Shape:
    def area(self):
        pass


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2


def main():
    """
    >>> [shape.area() for shape in [Rectangle(4, 5), Circle(7)]]
    [20, 153.86]
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### abstraction

Abstraction is an important concept in object-oriented programming (OOP) because it allows you to focus on the essential features of an object or system while ignoring the details that aren’t relevant to the current context. By reducing complexity and hiding unnecessary details, abstraction can make code more modular, easier to read, and easier to maintain.

```python
from abc import ABC, abstractmethod


class Shape(ABC):
    @abstractmethod
    def area(self):
        pass


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius


def main():
    """
    >>> [shape.area() for shape in [Rectangle(4, 5), Circle(7)]]
    Traceback (most recent call last):
    ...
    TypeError: Can't instantiate abstract class Circle without an implementation for abstract method 'area'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

---

### class diagram

In software engineering, a class diagram in the Unified Modeling Language (UML) is a type of static structure diagram that describes the structure of a system by showing the system's classes, their attributes, operations (or methods), and the relationships among objects.

<p align="center" width="100%">
    <img width="33%" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Uml_classes_en.svg/512px-Uml_classes_en.svg.png"> 
</p>

---

### method resolution order

```python
class A:
    def process(self):
        print('A')


class B(A):
    pass


class C(A):
    def process(self):
        print('C')


class D(B, C):
    pass


def main():
    """
    >>> D.__mro__
    (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
Note: a class can't be called before its superclass in resolving MRO. Super Class has to be called after derived class

---

### inheritance vs composition

*Inheritance* and *composition* are quite different concepts and they respond to different relationship between classes. If classes have a **is-a** relationship then *inheritance* is the right choice, if they have a **has-a** relationship then it’s a *composition*.

:bulb: *Inheritance*

```python
class Animal:
    def eat(self):
        pass

    def sleep(self):
        pass


class Bird(Animal):
    def fly(self):
        pass

    def sing(self):
        pass
```

:bulb: *Composition*

```python
class Salary:
    pass


class Employee:
    def __init__(self, salary):
        self.salary = salary


Employee(salary=Salary())
```

---

### staticmethod vs classmethod

|  :memo:   |                 Class Method                  |            Static Method            |
| :-------: | :-------------------------------------------: | :---------------------------------: |
| Decorator |                `@classmethod`                 |           `@staticmethod`           |
| Use Case  | More widely used as a factory method to class |      Acts as utility functions      |
|   Scope   |      Bound to the class and not objects       | Also bound to class and not objects |
| Behaviour |       Can modify the state of the class       |      Can't access class state       |
| Parameter |        Takes `cls` as first parameter         |        No specific parameter        |


```python
class Circle:
    no_of_circles = 0
    def __init__(self, radius):
        self.radius = radius
        Circle.no_of_circles += 1
        
    @staticmethod
    def square(num):
        return num**2
    
    @classmethod
    def getCircleCount(cls):
        return cls.no_of_circles
```

---

### class variable vs instance variable

|   :memo:    |                       Class Variable                        |        Instance Variable         |
| :---------: | :---------------------------------------------------------: | :------------------------------: |
| Declaration | Inside class definition but outside of any instance methods |     Inside `__init__` method     |
|    Scope    |                  Shared across all objects                  |   Tied to the object instance    |
|  Behaviour  |        Any change is reflected across all instances         | Change limited to instances only |
|   Access    |                     `cls.variable_name`                     |       `self.variable_name`       |


```python
class Car:
    total_cars, wheels = 0, 4

    def __init__(self, engine_power):
        self.engine_power = engine_power
        Car.total_cars += 1


car = Car(120)


def main():
    """
    >>> Car.total_cars
    1
    >>> car.wheels += 1
    >>> Car.wheels += 2
    >>> car.wheels
    5
    >>> Car.wheels
    6
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### mutable default parameter

The function parameters evaluate when the function is defined, not when it runs.

```python
from typing import List


class Student_v1:
    def __init__(self, name: str, grades: List[int] = []):  # this is bad!
        self.name = name
        self.grades = grades

    def take_exam(self, result):
        self.grades.append(result)


class Student_v2:
    def __init__(self, name: str, grades: List[int] = None):
        self.name = name
        self.grades = grades or []  # new list created if one isn't passed

    def take_exam(self, result):
        self.grades.append(result)


def main():
    """
    >>> bob = Student_v1("Bob")
    >>> rolf = Student_v1("Rolf")
    >>> bob.take_exam(90)
    >>> bob.grades
    [90]
    >>> # should be [], but it's [90]
    >>> rolf.grades 
    [90]
    >>> bob = Student_v2("Bob")
    >>> rolf = Student_v2("Rolf")
    >>> bob.take_exam(90)
    >>> bob.grades
    [90]
    >>> rolf.grades
    []
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

---

### monkey patching

The dynamic modifications made to a class or module at runtime are termed as monkey patching in Python. Most of the time it's a pretty terrible idea - it is usually best if things act in a well-defined way. One reason to monkey patch would be in testing. The mock package is very useful to this end.

```python
class Victim:
    def introduce(self):
        return self.__class__.__name__


def main():
    """
    >>> print(Victim().introduce())
    Victim
    >>> Victim.introduce = lambda self : "Patched"
    >>> print(Victim().introduce())
    Patched
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

---

### type hinting

Type checkers help ensure that you're using variables and functions in your code correctly.

```python

from typing import Dict, Generic, TypeVar

T = TypeVar("T", str, int)

class Registry(Generic[T]):
    def __init__(self) -> None:
        self._store: Dict[str, T] = {}

    def set_item(self, k: str, v: T) -> None:
        self._store[k] = v

    def get_item(self, k: str) -> T:
        return self._store[k]


def main():
    """
    >>> family_name_reg = Registry[str]()
    >>> family_age_reg = Registry[int]()
    >>> family_name_reg.set_item("dad", "John")
    >>> family_age_reg.set_item("John", 30)
    >>> family_name_reg.get_item("dad")
    'John'
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

:bulb: A type checker like `mypy` or`pyright` is a tool used to enforce type hinting in Python. 

```shell
pip install mypy
mypy .
```

```shell
pip install pyright    
pyright my_file.py
```

---

##  async and concurrency

### thread vs process

A thread is a lightweight, independent unit of execution that can run within a process. Threads within a process share the same memory space, making it easy for them to share data and communicate with each other. A process, on the other hand, is a self-contained execution environment that has its own memory space and resources.   

---

### cpu-bound vs i/o-bound tasks

- A CPU-bound task spends most of its time doing heavy calculations with the CPUs.
- An I/O-bound task spends most of its time waiting for I/O responses, which can be responses from web pages, databases or disks.

---

### global interpreter lock

The Python Global Interpreter Lock or GIL, in simple words, is a mutex (or a lock) that allows only one thread to hold the control of the Python interpreter.

This means that only one thread can be in a state of execution at any point in time. The impact of the GIL isn’t visible to developers who execute single-threaded programs, but it can be a performance bottleneck in CPU-bound and multi-threaded code.

Since the GIL allows only one thread to execute at a time even in a multi-threaded architecture with more than one CPU core, the GIL has gained a reputation as an “infamous” feature of Python.

```python
import time
from threading import Thread
from multiprocessing import Pool

COUNT = 50000000


def countdown(n):
    while n > 0:
        n -= 1


if __name__ == "__main__":
    # single thread
    start = time.time()
    countdown(COUNT)
    end = time.time()

    print(f'{round(end - start, 3)} - single thread')

    # multi thread
    t1 = Thread(target=countdown, args=(COUNT//2,))
    t2 = Thread(target=countdown, args=(COUNT//2,))

    start = time.time()
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    end = time.time()

    print(f'{round(end - start, 3)} - multi thread')

    # multi process
    pool = Pool(processes=2)
    start = time.time()
    r1 = pool.apply_async(countdown, [COUNT//2])
    r2 = pool.apply_async(countdown, [COUNT//2])
    pool.close()
    pool.join()
    end = time.time()

    print(f'{round(end - start, 3)} - multi process')
```

```python
# output
2.899 - single thread
2.876 - multi thread
1.582 - multi process
```

Multiprocessing might be a solution, but multiple processes are heavier than multiple threads, so, keep in mind that this could become a scaling bottleneck.

---

### race condition

A race condition occurs when multiple threads access shared data or resources simultaneously, and the outcome of the program depends on the order in which the threads execute. Thread safety is the property of an application or library that it can handle multiple threads accessing shared data or resources without introducing race conditions.

```python
from threading import Thread

x = 1


def fibonacci(n):
    if n <= 2:
        return 1
    return fibonacci(n-1) + fibonacci(n-2)


def example():
    global x
    while x <= 10:
        print(fibonacci(x))
        x += 1


t1 = Thread(target=example)
t2 = Thread(target=example)
t1.start()
t2.start()
t1.join()
t2.join()

```
```python
# cause an issue with the calculation
1
1
2
1
5
8
3
21
13
34
55
```

Some mechanisms for synchronizing access to shared resources include:

- **Locks**: a mechanism that allows only one thread to execute a critical section of code at a time.
- **Semaphores**: a mechanism that allows multiple threads to access a shared resource, but with a limit on the number of threads that can access the resource at the same time.
- **Monitors**: a mechanism that allows only one thread to execute a critical section of code at a time, and also provides a mechanism for threads to wait for specific conditions to be met before continuing execution.

```python
from threading import Thread, Lock, Semaphore

x, y = 1, 1
lock = Lock()
semaphore = Semaphore(1)


def fibonacci(n):
    if n <= 2:
        return 1
    return fibonacci(n-1) + fibonacci(n-2)


def example_lock():
    global x
    with lock:
        while x <= 10:
            print(fibonacci(x))
            x += 1


def example_semaphore():
    global y
    semaphore.acquire()
    while y <= 10:
        print(fibonacci(y))
        y += 1
    semaphore.release()


def test_lock():
    t1, t2 = Thread(target=example_lock), Thread(target=example_lock)
    t1.start()
    t2.start()
    t1.join()
    t2.join()


def test_semaphore():
    t1, t2 = Thread(target=example_semaphore), Thread(target=example_semaphore)
    t1.start()
    t2.start()
    t1.join()
    t2.join()


def main():
    """
    >>> test_lock()
    1
    1
    2
    3
    5
    8
    13
    21
    34
    55
    >>> test_semaphore()
    1
    1
    2
    3
    5
    8
    13
    21
    34
    55
    """


if __name__ == '__main__':
    import doctest
    doctest.testmod()

```

---

### asyncio

Asyncio is a Python library for asynchronous programming, which provides the infrastructure for writing single-threaded concurrent code using coroutines, event loops, and non-blocking I/O. 

```python
import asyncio


async def async_func(id):
    print(f'[{id}] Hello ...')
    await asyncio.sleep(1)
    print(f'[{id}] ... World!')


async def example(id):
    # Coroutines are generally used for cooperative tasks and behave like Python generators
    await async_func(id)


async def example_with_task(id):
    # Tasks are used to schedule coroutines concurrently
    await asyncio.create_task(async_func(id))


async def example_with_even_loop():
    # An event loop manages and distributes the execution of different tasks.
    # It registers them and handles distributing the flow of control between them.
    tasks = [loop.create_task(async_func(x + 2)) for x in range(2)]
    await asyncio.wait(tasks)


def main():
    """
    >>> asyncio.run(example(0))
    [0] Hello ...
    [0] ... World!
    >>> asyncio.run(example_with_task(1))
    [1] Hello ...
    [1] ... World!
    >>> loop.run_until_complete(example_with_even_loop())
    [2] Hello ...
    [3] Hello ...
    [2] ... World!
    [3] ... World!
    """

if __name__ == "__main__":
    loop = asyncio.new_event_loop()
    asyncio.set_event_loop(loop)

    import doctest
    doctest.testmod()

    loop.close()
```

---

### async context manager

The async with statement is used for managing resources in an asynchronous context, similar to the regular with statement for synchronous code. It's commonly used for working with asynchronous I/O resources that need to be acquired and released safely.

```python
import asyncio


class MyAsyncContextManager:
    async def __aenter__(self):
        print("ENTER async with")

    async def __aexit__(self, *args):
        print("EXIT async with")


async def demo():
    async with MyAsyncContextManager() as cm:
        print("BODY async with")


def main():
    """
    >>> asyncio.run(demo())
    ENTER async with
    BODY async with
    EXIT async with
    """


if __name__ == '__main__':
    import doctest
    doctest.testmod()

```

---
### future object

The Future class encapsulates the asynchronous execution of a callable. Future instances are created by `Executor.submit()`.

```python
from concurrent.futures import ThreadPoolExecutor


def main():
    """
    >>> with ThreadPoolExecutor(max_workers=1) as executor:
    ...     future = executor.submit(pow, 2, 10)
    ...     print(future.result())
    1024
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

---

## References
- Fluent Python - Luciano Ramalho
