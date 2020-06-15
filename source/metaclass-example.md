---
title: metaclass example
date: 2020-05-07
---
Example Python program metaclass-example.py
For Python version 2.x.
To test your Python version use:

    python --version


## Classes

* class Meta(type):
* print 'Initializing class %s (%r): %r' %(
* class A(object):

## Methods

* def __new__(metacls, name, parents, attrs):
* def __init__(cls, name, parents, attrs):
* def __init__(self, a):
* def foo(self):

## Code

Python example

    '''
    A simple example with Python metaclasses:
    Add a class attribute to all classes from this metaclass
    '''
    
    class Meta(type):
     
        def __new__(metacls, name, parents, attrs):
            print 'Creating class %s ...' %(name)
            # Create a new instance of type (i.e. a class!) 
            return type.__new__(metacls, name, parents, attrs)
        
        def __init__(cls, name, parents, attrs):
            print 'Initializing class %s (%r): %r' %(
                cls.__name__, ','.join([p.__name__ for p in parents]), attrs.keys())
            # Complete default initialization
            type.__init__(cls, name, parents, attrs)
            # Add a class attribute for all classes in this family (metaclass)
            cls.baz = 42
    
    class A(object):
        __metaclass__ = Meta
    
        def __init__(self, a):
            self.a = a
    
        def foo(self):
            return self.a
    
    a = A(19)
    
    print 'a.baz=', a.baz
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
