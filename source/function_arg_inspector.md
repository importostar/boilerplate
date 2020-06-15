---
title: function_arg_inspector
date: 2020-05-07
---
Example Python program function_arg_inspector.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import collections
* import functools
* import inspect

## Methods

* def log_func_args(func):
* def decorator(*args, **kwargs):
* def test(a, b, c, d, e=99, f=33):

## Code

Python example

    # python3.5
    def log_func_args(func):
        import collections
        import functools
        import inspect
        
        @functools.wraps(func)
        def decorator(*args, **kwargs):
            parameters = inspect.signature(func).parameters
            param_args = collections.OrderedDict({
                k: v.default for k, v in parameters.items()
            })
            arg_iter = iter(args)
            for param in param_args.keys():
                try:
                    param_args[param] = next(arg_iter)
                except StopIteration:
                    break
            param_args.update(kwargs)
    
            print(
                '{}({})'.format(
                    func.__name__,
                    ', '.join('{}={}'.format(k, v) for k, v in param_args.items())
                )
            )
            return func(*args, **kwargs)
        return decorator
    
    
    @log_func_args
    def test(a, b, c, d, e=99, f=33):
        return a, b, c, d, e , f
    
      
    In [1]: test(1, 2, 3, 4)
    test(a=1, b=2, c=3, d=4, e=99, f=33)
    Out[1]: (1, 2, 3, 4, 99, 33)
    
    In [2]: test(1,2,3, 4, e=5, f=6)
    test(a=1, b=2, c=3, d=4, e=5, f=6)
    Out[2]: (1, 2, 3, 4, 5, 6)
      
    In [3]: test(1, 2, 3, 4, f=6, e=5)
    test(a=1, b=2, c=3, d=4, e=5, f=6)
    Out[3]: (1, 2, 3, 4, 5, 6)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
