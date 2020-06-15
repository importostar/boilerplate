---
title: descriptor
date: 2020-05-07
---
Example Python program descriptor.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class Name:
* class Technician:
* class Engineer:

## Methods

* def __get__(self, instance, owner):
* def __set__(self, instance, value):
* def __delete__(self, instance):
* def __init__(self, name) -> None:
* def __init__(self, name) -> None:

## Code

Python example

    # descriptor, is like a simplification on property
    # one descriptor can be used in multiple classes, instead of repeated property definitions
    
    class Name:
        def __get__(self, instance, owner):
            print(instance, 'get name')
            return instance._name
        def __set__(self, instance, value):
            print(instance, 'set name to', value)
            instance._name = value
        def __delete__(self, instance):
            del instance._name
    
    class Technician:
        def __init__(self, name) -> None:
            self._name = name
        name = Name()
    
    class Engineer:
        def __init__(self, name) -> None:
            self._name = name
        name = Name()
    
    
    t = Technician('jj')
    e = Technician('dd')
    
    print(t.name)
    print(e.name)
    
    t.name = 'jack'
    e.name = 'dela'
    
    # output: #
    #>> <__main__.Technician object at 0x0000000002935F60> get name
    #>> jj
    #>> <__main__.Technician object at 0x0000000002934320> get name
    #>> dd
    #>> <__main__.Technician object at 0x0000000002935F60> set name to jack
    #>> <__main__.Technician object at 0x0000000002934320> set name to dela

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
