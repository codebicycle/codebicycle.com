# Python

[PyPI - the Python Package Index][pypi]  
[The Hitchhiker’s Guide to Python][hitchhiker]

[pypi]: https://pypi.python.org/pypi
[hitchhiker]: http://docs.python-guide.org/en/latest/

***

Virtual environment
    
    :::bash
    # virtualenvwrapper
    mkvirtualenv --python=`which python3` EnvName
    workon EnvName

    # Python's venv module
    python3 -m venv virtual_environment_name
    # -m module-name
    cd virtual_environment_name
    source bin/activate

***

Python’s default arguments are evaluated once when the function is defined, not each time the function is called.
    
    :::python
    def append_to(element, to=[]):
      to.append(element)
      return to

    my_list = append_to(12)
    print my_list

    my_other_list = append_to(42)
    print my_other_list

    # [12]
    # [12, 42]

A new list is created once when the function is defined, and the same list is used in each successive call.

What you should do instead:
    
    :::python
    def append_to(element, to=None):
        if to is None:
            to = []
        to.append(element)
        return to

***

Python’s closures are late binding. This means that the values of variables used in closures are looked up at the time the inner function is called.

***

`+` operator creates a new object

    :::python
    path = []
    path = path + [start]   # creates a new list

***

If `send` has multiple recipients, it is better to define it explicitly: `send(message, recipients)`  and call it with `send('Hello', ['God', 'Mom', 'Cthulhu'])` than `send(message, *args)`. This way, the user of the function can manipulate the recipient list as a list beforehand, and it opens the possibility to pass any sequence, including iterators, that cannot be unpacked as other sequences.

***

If it's not unique to an instance, it doesn't belong to an instance variable.

***

Lambda's (make function) syntax is similar to def, but leaves out:

- name of the function
- parameters parenthesis
- return keyword

```python
def fn(a, b, c):
    return a + b + c
  
lambda a, b, c: a + b + c
```

***

Floor division `x.__floordiv__(y)`
    
    :::python
    x // y
    
Floor division and modulo
    
    :::python
    divmod(x, y)

***

`else` in loops
    
    :::python
    for:
        ...
    else:   # no break (loop not terminated by a break statement)
        ...

***

Simultaneous state update

- eliminates out of order update errors
- allows high level thinking

```python
x, y = y, x + y

x, y, dx, dy = (x + dx * t,
                y + dy * t,
                ... ,
                ...)
```
***

Use decorators to factor out administrative logic
    
    :::python
    @cache
    def web_lookup(url):
        return urllib.urlopen(url).read()


    def foo():
        # do something

    def decorator(func):
        # manipulate func
        return func

    foo = decorator(foo)  # Manually decorate

    @decorator
    def bar():
        # Do something
    # bar() is decorated


***

Context manager
    
    :::python
    from contextlib import suppress
    with suppress(FileNotFoundError):
        os.remove('somefile.tmp')


***

Raymond Hettinger - [Transforming Code into Beautiful, Idiomatic Python][idiomatic]

[idiomatic]: https://www.youtube.com/watch?v=OSGv2VnC0go

    import functools
    import operator
    functools.reduce(operator.add, range(10))    # ((0 + 1) + 2) + 3 ...
    sum(range(10))

    >>> map(str, range(10))
    >>> next(_)   # _ result of last invocation
    map(lambda m: m.name, sequence)

    filter(lambda x:x > 0, [0, -1, 3, 4, -2])   # <filter at 0x7f...> [3, 4]

***

Named slices
    
    :::python
    name = slice(0, 10)
    lastname = slice(10, 20)
    line[name], line[lastname]


***

- Assertions are not for error handling (like checking arguments, we have exceptions for that)
- Assert results of implementation logic are sane `assert result >= 0`
- Asserts should only fail if the code is wrong
- Assertions can be turned off

***

`random.choices` selects with replacement (puts it back in urn before next draw)

    from random import choices, sample
    sample([1,2,3], k=3)    # [1, 2, 3]
    choices([1,2,3], k=3)   # [1, 1, 1]

***

Do while construct
    
    :::python
    while True:
        stuff()
        if fail_condition:
            break

***

`sys.path` current search path (imports).

***

`timeit` module

```python
from timeit import Timer

def get_digits1(text):
    c = ""
    for i in text:
        if i.isdigit():
            c += i
    return c

def get_digits2(text):
    return filter(str.isdigit, text)

def get_digits3(text):
    return ''.join(c for c in text if c.isdigit())

if __name__ == '__main__':
    count = 5000000
    t = Timer("get_digits1('abcdef123456789ghijklmnopq123456789')",
              "from __main__ import get_digits1")
    print t.timeit(number=count)

    t = Timer("get_digits2('abcdef123456789ghijklmnopq123456789')",
              "from __main__ import get_digits2")
    print t.timeit(number=count)

    t = Timer("get_digits3('abcdef123456789ghijklmnopq123456789')", 
              "from __main__ import get_digits3")
    print t.timeit(number=count)

# 19.990989106  # Your original solution
# 16.7035926379 # Mine solution
# 24.8638381019 # Accepted solution
```

## Debugging
    
    :::yaml
    python -i file.py
    ipython -i file.py      # inspect interactively after running script
    python -m pdb script.py       # post-mortem (on exceptions)
    import pdb; pdb.pm()          # pdb post-mortem
    import pdb; pdb.set_trace()   # manual breakpoint
      help
      continue  # next breakpoint
      next      # next line, current context
      step      # next, step into functions
      list      # show context
      up
      return
      bt

    from IPython import embed; embed()

    type()
    callable('mystring'.__add__)
    True.__class__
    True.__class__.__bases__
    bool.__mro__
    inspect.getmro(type(True))
    dir(5.0)
    id(obj)
    a is b
    del a   # Remove a from the namespace
    del     # keyword
    locals()

    python -m cProfile script.py
    import cProfile
    cProfile.run('test()')

Method Resolution Order or MRO

    >>> pprint(LoggingOD.__mro__)
    (<class '__main__.LoggingOD'>,
     <class '__main__.LoggingDict'>,
     <class 'collections.OrderedDict'>,
     <class 'dict'>,
     <class 'object'>)

    >>> LoggingOD.__bases__
    (LoggingDict, OrderedDict)


`super()` calls parents or ancestors of your children.  
`super()` means "next in line" (method resolution order).

- children get called before their parents
- parents stay in order

[Python’s super() considered super!][super-hettinger] by Raymond Hettinger

[super-hettinger]: https://rhettinger.wordpress.com/2011/05/26/super-considered-super/


Debugging pretty printing
    
    :::python
    print(json.dumps(obj, indent=4, sort_keys=True))

    any_list = [1, 2, 3]
    dir(any_list)
    help(any_list.reverse)

Place breakpoints in except clauses

    try:
      # code
    except ValueError:
      import pdb; pdb.set_trace()

    from itertools import chain
    flatten = chain.from_iterable
    nested = [[1,2], [3,4], [4,5]]
    flatten(nested)   # 1, 2, 3, 4, 5

    def trace(f):
        "Print a trace of the input and output of a function on one line."
        def traced_f(*args):
            result = f(*args)
            print('{}({}) = {}'.format(
              f.__name__, 
              ', '.join(map(str, args)), result)
            )
            return result
        return traced_f

## Logging

    import logging
    # logging.basicConfig(level=logging.DEBUG)  # default WARNING

    logging.debug('debug message')
    logging.info('info message')
    logging.warning('warning message')


## Testing
    :::bash
    unittest      # standard lib
    unittest.mock
    pytest
    pytest --pdb  # Dropping to PDB (Python Debugger) on failures

Pycharm debug tests

1.  Set breakpoints
2.  Attach debugger in python console
3.  Import and call pytest  

        import pytest
        pytest.main(args=[__file__])

***

Extract the functionality that doesn't need to talk to the database to a separate method and test it separately.

## Jupyter Notebook
    :::yaml
    ! ls -l     # shell commands
    % magic
    %% time     # single run
    %% timeit   # multiple runs
    %% prun     # profiling

## Django

Model field arguments

`null`: If True, Django will store blank values as NULL in the database for fields where this is appropriate (a CharField will instead store an empty string). The default is False.

`blank`: If True, the field is allowed to be blank in your forms. The default is False, which means that Django's form validation will force you to enter a value. This is often used with null=True , because if you're going to allow blank values, you also want the database to be able to represent them appropriately.

***

    {% block title %}Login | {{ block.super }}{% endblock title %}


## Beyond PEP 8 by Raymond Hettinger

- recognize non-pythonic APIs
- don't get distracted by PEP 8, focus first on Pythonic versus NonPythonic
- when needed write an adapter class
- avoid unnecessary packaging in favor of simpler imports
- create custom exceptions
- use properties instead of getter methods
- create a context manager for recurring set-up and teardown logic
- use magic methods: `__len__`, `__getitem__`
- add good `__repr__` for better debuggability

        :::python
        def __repr__(self):
            return '{}({})'.format(self.__class__.__name__, self.data)



## Design Patterns with Python - Pluralsight

Interface - Abstract Base Class

- Behavioral
    - Strategy Pattern
    - Observer Pattern



## Unit TEsting with Python - Pluralsight

Unit tests run in memory.

It's not unit test if it uses...

  - the file system
  - a database
  - the network
  - external dependencies
  - deployment

Regression - something that used to work, doesn't anymore.

Test Double - like 'Stunt Double'

  - Test Stub     (hard codded answer)
  - Fake Object   (real implementation, yet unsuitable for production)
  - Mock Object   (was method called?)
  - Test spy      (query afterwards what happened)
  - Dummy Object  (interface requires an argument, not used by the test)

Three kinds of Assert

- Check the return value or an exception
- Check a state change (public API)
- Check a method call (mock or spy)

Monkey Patching



## Python Epiphanies - Safari

> A decorator changes or adds to the functionality of a function either by
> modifying its arguments before the function is called, or changing its return
> value afterwards, or both.

Decorators

- pass the body of the defined function to the decorator function
- modify namespace, the name of the defined function points to the decorator function's return value


## Designing Data Structures in Python, George T. Heineman - Safari
    
    :::python
    def getMin(self):
        if self.root is None:
            raise ValueError('Binary Tree is empty')
        n = self.root
        while n.left:
            n = n.left
        return n.value


## Python Beyond The Basics - Object Oriented Programming

Object attribute lookup hierarchy

- instance
- class
- any class from which the class inherits

## Python Data Structures - Safari

    if 'key' not in dictionary:
        dictionary['key'] = set()
    dictionary['key'].add('value')

    dictionary.setdefault('key', set()).add('value')

    from collections import defaultdict

    set.remove(item)
    set.discard(item)   # no KeyError
    frozenset()         # imutable


## Python Programming Language, David Beazley - Safari  
    
    :::python
    for idx, item in enumerate(items, start=1):
        pass

    getattr(obj, 'name')        # obj.name
    setattr(obj, 'cost', 10)    # obj.cost = 10
    del obj.name
    obj.__dict__
    obj.__class__.__dict__
    vars(obj.__class__)

    @property
    @price.setter

    after(5, lambda: greeting('Guido'))

    func.__name__


## Dive into Python3

Separate code from data.  
e.g. Pluralization rules are data, they belong in a separate file.

Implement cache.

## Modern Python by Raymond Hettinger

Lambda

- make function
- defer computation, make a promise  
  Run a computation at some point in the future

        :::python
        f = lambda : x ** y
        f()


`zip *` means transpose

    zip(*data)


defaultdict

- use for grouping data (list, set)
- accumulation
- reverse one-to-many mapping


Expand wildcard

    glob.glob('*.txt')


Wrap in csv reader

    import csv
    with open('file.csv') as f:
        for row in csv.reader(f):
            print(row)


## Python: Programming efficiently - Lynda.com
    :::python
    itertools.chain(iter1, iter2)   # concatenate
    i1, i2 = itertools.tee(iter, 2) # duplicate
    itertools.accumulate(iter)      # running sum
    itertools.product(iter1, iter2) # element-by-element product


Sets cannot have a mutable element, like list, set or dictionary, as its elements.

***

`x and y` first evaluates x; if x is false, its value is returned; otherwise, y is evaluated and the resulting value is returned.

`x or y` first evaluates x; if x is true, its value is returned; otherwise, y is evaluated and the resulting value is returned.

Note that neither `and` nor `or` restrict the value and type they return to False and True, but rather return the last evaluated argument.

***

Python Data Structures - Safari

Object attributes without underscores
    
    :::python
    any_dict = {}
    [attr for attr in dir(any_dict) if '__' not in attr]




## Working with Algorithms in Python, by George Heineman - Safari

- binary array search
- binary search tree
- balanced binary search tree
- mergesort
- exponentiation by squaring
- peg solitaire
- magic squares

Graph representation

- adjacency matrix (dense edges)
- adjacency list (sparse edges)

Shortest path in a graph

- Dijkstra - flood fill 
- A* - use heuristic

Dynamic programming

- solve small, constrained versions of problem
- systematically relax constraints until solution

e.g. Shortest path, minimum cost (by generating all pairs shortest paths)

Floyd Warshall algorithm

1. Include weights of arcs in graph as a best short estimate; add 0 on the diagonal and infinity where there is no arc (adjacency matrix); smallest constrained version of problem.
2. Relax the constraints. First allow path to include vertex v0. Check if traveling through v0 has a lower cost than the direct arc. Then allow path to include each node, one by one.
3. Use another predecessor array to recreate paths.



## Python Design Patterns - [Safari video][pdp-safari]

overriding - different implementation of a method defined in a superclass  
overloading - method with the same name but different arguments

interface - defines just the methods  
abstract base class - may also define attributes

Creational Patterns  
Abstract the task of creating of an object from the details of creating it.

- Factory - create objects from a family of related objects (know at runtime which type)
- Builder - complex objects
- Prototype - objects with costly creation (clone instead of `__init__`)
- Singleton and Borg - only one instance or shared state

Structural Patterns

- MVC - separation of concerns in UIs
- Facade - abstract complexities of subsystems
- Proxy - control or alter access to a certain class
- Decorator - dynamic runtime composition
- Adapter - make two incompatible interfaces work together


[pdp-safari]: http://proquestcombo.safaribooksonline.com.ezproxy.torontopubliclibrary.ca/video/programming/python/9781786460677


## [Problem Solving with Algorithms and Data Structures using Python][problem-solving-interactive]

Stack, LIFO

- ordering based on length of time in the collection
- removal order is the reverse order of insertion
- can be used to reverse order of items

Queue, FIFO

Deque

- items are added and removed from either end

Convert decimal numbers to binary

- Divide by 2 and keep track of the remainder, reverse remainders
- Divide by base (general)

[problem-solving-interactive]:http://interactivepython.org/runestone/static/pythonds/index.html


## Data Visualization Basics with Python

- Clearly define the **story**  
  What should the visualization communicate?

- Pick the right chart  
   What charts tells the story more clearly without adding to much information?

- Assess your visualization  
  Can you immediately see the story?  
  Are there distractions?

Minimal

- use multiple colors only when color adds more information
    - color schemes: qualitative, sequential, diverging http://colorbrewer2.org
    - color blindness
    - print well B&W
- 3D charts? Does it add more data? No!
- keep it simple
- no chart junk

Types

- bar
- line chart
- pie chart
- stacked areas (trends)
- histogram
- scatter plots

CDF cumulative distribution function

WTF http://viz.wtf  
http://reddit.com/r/dataIsUgly


## Modular Programming with Python - [Safari][modular-python]  
Code examples, architecture

- Breakdown program functionality

    e.g. Inventory system

    - Storing information
    - Interacting with the user
    - Generationg reports


[modular-python]: http://proquestcombo.safaribooksonline.com.ezproxy.torontopubliclibrary.ca/book/programming/python/9781785884481


## Resources

Design of Computer Programs by Peter Norvig - [Udacity ][design-norvig]

Web Scraping with Python by Richard Lawson

Learning Scrapy by Dimitrios Kouzis-Loukas

Intermediate Django - [Safari][intermediate-django]

Learning Python Application Development - [Safari][python-application-dev]

  * design patterns (pythonic vs NonPythonic)
  * strategy
  * simple factory
  * abstract factory

Enterprise Software with Python

  * [pythontesting.net](http://pythontesting.net/)
  * [pythondoeswhat.blogspot.com](http://www.pythondoeswhat.com/)
  * [Planet Python](http://planetpython.org/)
  * [interactivepython.org](http://interactivepython.org)
  * [Python Koans](https://github.com/gregmalcolm/python_koans)


Intermediate Python Programming - Safari

Code Dojo TDD - Pluralsight

Effective Python - Safari

Two Scoops of Django: Best Practices for Django 1.8

Elasticsearch Essentials - Safari

Python Machine Learning Projects - Safari

Python Data Visualization Solutions - Safari

 - Importing data (csv, fixed width, etc.)



[design-norvig]: https://eu.udacity.com/course/design-of-computer-programs--cs212

[intermediate-django]: http://proquestcombo.safaribooksonline.com.ezproxy.torontopubliclibrary.ca/video/web-development/django/9781771374101

[python-application-dev]: http://proquestcombo.safaribooksonline.com.ezproxy.torontopubliclibrary.ca/book/programming/python/9781785889196
