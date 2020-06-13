---
title: python_src_decorators_attribute
date: 2020-05-07
---
Example Python program python_src_decorators_attribute.py


## Classes

* class Attribute(object):
* class Sample:

## Methods

* def __init__ (self, getter, setter = None, deleter = None):
* def __set__ (self, instance, value):
* def __get__ (self, instance, cls):
* def setter (self, fn):
* def getter (self, fn):
* def deleter (self, fn):
* def __init__ (self):
* def name (self):
* # def test (self, value):

## Code

Python example

    class Attribute(object):
        __slots__ = ['fset', 'fget', 'fdel', 'name', 'value']
    
        def __init__ (self, getter, setter = None, deleter = None):
            self.fget = getter
            self.fset = setter
            self.fdel = deleter
            self.name = getter.__name__
            self.value = None
    
        def __set__ (self, instance, value):
            if self.fset is None:
                self.value = value
            else:
                self.fset(instance, value)
    
        def __get__ (self, instance, cls):
            result = self.fget(instance)
            if result is None and self.fset is not None:
                raise NotImplementedError('Attribute \'%s\' has setter(), but not impletement getter method' % (self.name))
            elif result is not None and self.fset is None:
                raise NotImplementedError('Attribute \'%s\' has getter(), but not impletement setter method' % (self.name))
            return result or self.value
    
        def setter (self, fn):
            self.fset = fn
            return self
    
        def getter (self, fn):
            self.fget = fn
            return self
    
        def deleter (self, fn):
            self.fdel = fn
            return self
    
    
    if __name__ == '__main__':
        class Sample:
            def __init__ (self):
                self._name = 'This is the get text from Test'
                pass
    
            @Attribute
            def name (self):
                pass
                # return self._name
    
            # @name.setter
            # def test (self, value):
            #     self._name = value
    
    
        x = Sample()
        print x.name
    
        x.name = 'tsdt'
        print x.name
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
