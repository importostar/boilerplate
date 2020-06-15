---
title: call_after
date: 2020-05-07
---
Example Python program call_after.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import typing

## Classes

* class CallAfter:

## Methods

* def __init__(self, times: int) -> None:
* def __call__(self, _function: typing.Callable, *args, **kwargs):
* def new_function(*args_, **kwargs_):
* def foo_bar(value):
* def bar_foo(value):
* def main():

## Code

Python example

    #!/usr/bin/python3
    
    """
        Python: Created by Naman Jain on 22-01-2018
        File: call_after.py
    
        This script for calling a function after calling it for specified numbers of time
    
    """
    import typing
    
    
    class CallAfter:
        """
            Class for creating functions which are actually called after
            being called a certain number of times
        """
    
        def __init__(self, times: int) -> None:
            super().__init__()
            self.to_be_called_after = times
            self.__called = 0
    
        def __call__(self, _function: typing.Callable, *args, **kwargs):
            def new_function(*args_, **kwargs_):
                """
                    decorated function
                :param args_:
                :type args_:
                :param kwargs_:
                :type kwargs_:
                """
                if self.__called >= self.to_be_called_after:
                    temp = self.__called
                    print(f"Called: {temp} -> ", end="")
                    _function(*args_, **kwargs_)
    
                self.__called += 1
    
            return new_function
    
    
    @CallAfter(4)
    def foo_bar(value):
        """
            foo function
        """
        print(f"foo: {value}")
    
    
    @CallAfter(5)
    def bar_foo(value):
        """
            bar function
        """
        print(f"bar: {value}")
    
    
    def main():
        """
            Main Function
        """
        foo_bar("Python")  # 1
        bar_foo("Python")  # 1
    
        foo_bar("Python")  # 2
        bar_foo("Python")  # 2
    
        foo_bar("Python")  # 3
        bar_foo("Python")  # 3
    
        foo_bar("Python")  # 4
        bar_foo("Python")  # 4
    
        foo_bar("Python")  # 5
        bar_foo("Python")  # 5
    
        bar_foo("Python")  # 6
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
