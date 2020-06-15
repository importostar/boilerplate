---
title: Python_Descriptors
date: 2020-05-07
---
Example Python program Python_Descriptors.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class MyDescriptor():
* class MyClass():

## Methods

* def __init__(self, initial_value=None, name='my_var'):
* def __get__(self, obj, objtype):
* def __set__(self, obj, value):

## Code

Python example

    '''
    Provide the ability to add managed attributes to objects. 
    The methods needed to create a descriptor are __get__, __set__ and __delete__.
    If you define any of these methods, then you have created a descriptor.
    Idea is to get, set or delete attributes from your object’s dictionary. 
    When you access a class attribute, this starts the lookup chain
    
    __get__(self, obj, type=None), returns value
    __set__(self, obj, value), returns None
    __delete__(self, obj), returns None
    
    defined at least one, you have created a descriptor
    define both __get__ and __set__, you will have created a data descriptor
    descriptor with only __get__() defined are known as non-data descriptors and are usually used for methods. 
    Read-only descriptor if you define both __get__ and __set__, but raise an AttributeError when the __set__ method is called.
    
    
    Why Descriptors ?
    Consider an email attribute. Verification of the correct email format is necessary before assigning a value to that attribute. 
    This descriptor allows email to be processed through a regular expression and its format validated before assigning it to an attribute.
    In many other cases, Python protocol descriptors control access to attributes, such as protection of the name attribute.
    '''
    
       
    class MyDescriptor():
        """
        A simple demo descriptor
        """
        def __init__(self, initial_value=None, name='my_var'):
            self.var_name = name
            self.value = initial_value
     
        def __get__(self, obj, objtype):
            print('Getting', self.var_name)
            return self.value
     
        def __set__(self, obj, value):
            msg = 'Setting {name} to {value}'
            print(msg.format(name=self.var_name, value=value))
            self.value = value
     
    class MyClass():
        desc = MyDescriptor(initial_value='Mike', name='desc')
        normal = 10
     
    if __name__ == '__main__':
        c = MyClass()
        print(c.desc)
        print(c.normal)
        c.desc = 100
        print(c.desc)
        
    
    # Source - https://www.ibm.com/developerworks/library/os-pythondescriptors/
    # https://www.blog.pythonlibrary.org/2016/06/10/python-201-what-are-descriptors/

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
