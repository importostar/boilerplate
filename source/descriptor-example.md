---
title: descriptor example
date: 2020-05-07
---
Example Python program descriptor-example.py


## Classes

* class alias(object):
* class distance(object):
* class A(object):

## Methods

* def __init__(self, field_name):
* def __get__(self, obj, objtype):
* def __set__(self, obj, value):
* def __init__(self, val):
* def __get__(self, obj, objtype):
* def __set__(self, obj, val):
* def alpha(self):
* def __init__(self, alpha):

## Code

Python example

    class alias(object):
    
        def __init__(self, field_name):
            self.field_name = field_name
        
        def __get__(self, obj, objtype):
            return getattr(obj, self.field_name)
        
        def __set__(self, obj, value):
            raise AttributeError('Cannot set attribute')
    
    class distance(object):
    
        def __init__(self, val):
            self.defaultval = float(val)
        
        def __get__(self, obj, objtype):
            return getattr(obj, '_distance', self.defaultval)
        
        def __set__(self, obj, val):
            setattr(obj, '_distance', max(.0, float(val)))
    
    class A(object):
    
        l = distance(1.7)
    
        a = alias('alpha')
    
        @property
        def alpha(self):
            return self._alpha
        
        def __init__(self, alpha):
            self._alpha = alpha
    
    
    a1 = A(19)
    a1 = A(29)
    
    print a1._alpha # via instance attribute
    print a1.alpha  # via intance property
    print a1.a # via data read-only descriptor
    print a1.l # via data read-write descriptor
    
    a1.l = 12.5
    a2.l = 19.7
    
    a1._alpha = 29
    
    
    try:
        a1.a = 39 # error! is read-only descriptor
    except AttributeError:
        pass
    
    try:
        a1.alpha = 29 # error! is read-only property
    except AttributeError:
        pass
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
