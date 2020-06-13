---
title: python_src_get_getattr_getattribute
date: 2020-05-07
---
Example Python program python_src_get_getattr_getattribute.py
For Python version 2.x.
To test your Python version use:

    python --version


## Classes

* class C(object):
* class C2(object):

## Methods

* def __init__(self):
* def __getattribute__(self, name):
* def __getattr__(self, name):
* def __get__(self, instance, owner):
* def foo(self, x):

## Code

Python example

    class C(object):
    
        def __init__(self):
            self.a = None
            # self.z = None
    
        def __getattribute__(self, name):
            print("__getattribute__() is called")
            return object.__getattribute__(self, name)
    
        def __getattr__(self, name):
            print("__getattr__() is called ")
            return name + " from getattr"
    
        def __get__(self, instance, owner):
            print("__get__() is called", instance, owner)
            return self
    
        def foo(self, x):
            print(x)
    
    
    class C2(object):
        d = C()
    
    
    if __name__ == '__main__':
        print '1 >>>'
        c = C()
    
        print '2 >>>'
        c2 = C2()
    
        print '3 >>> get exist attr \'c.a\''
        print(c.a)
    
        print '4 >>> get not exist attr  \'c.z\''
        print(c.z)
    
        print '5 >>> c2.d'
        c2.d
    
        print '6 >>> c2.d.a'
        print(c2.d.a)
    
        print '7 >>> c2.d.z'
        print(c2.d.z)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
