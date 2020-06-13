---
title: Snipplr 25256
date: 2020-05-07
---
Example Python program Snipplr-25256.py


## Classes

* &gt;&gt;&gt; class test(object):

## Methods

* ... def printNum(self):

## Code

Python example

    ## Every object in Python has an identity, a type, and a value. The identity points to the object's location in memory. The type describes the representation of the object to Python. The value of the object is simply the data stored inside.
    
    ## The following example shows how to access the identity, type, and value of an object programmatically using the id(object), type(object), and variable name, respectively:
    
    &gt;&gt;&gt; l = [1,2,3]
    &gt;&gt;&gt; print id(l)
    9267480
    &gt;&gt;&gt; print type(l)
    &lt;type 'list'&gt;
    &gt;&gt;&gt; print l
    [1, 2, 3]
    
    
    ## After an object is created, the identity and type cannot be changed. If the value can be changed, it is considered a mutable object; if the value cannot be changed, it is considered an immutable object.
    
    ## Some objects may also have attributes and methods. 
    ## Attributes are values associated with the object. Methods are callable functions that perform an operation on the object. 
    ## Attributes and methods of an object can be accessed using the following dot '.' syntax:
    
    &gt;&gt;&gt; class test(object):
    ...     def printNum(self):
    ...         print self.num
    ...
    &gt;&gt;&gt; t = test()
    &gt;&gt;&gt; t.num = 4
    &gt;&gt;&gt; t.printNum()
    4

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
