---
title: decorate
date: 2020-05-07
---
Example Python program decorate.py
For Python version 2.x.
To test your Python version use:

    python --version


## Methods

* def f():
* def f():
* def gg(xx):
* def s(y):
* def ff(x):
* def gg(func):
* def hh(y):
* def ff(x):
* def gg(func):   # decorator
* def hh(*args, **kwargs):# params must catch all args of ff
* def ff(*args, **kwargs):
* def f():
* def f():
* def gg(num):
* def h1(f1):
* def h2(f2):
* def ff(x):

## Code

Python example

    #/usr/bin/env python
    
    # ex1.py      
    
    @g
    def f():
        print("xyz")
    
    # is equivalent to                                                                                                                                    
    def f():
        print("xyz")
    f = g(f)
    
    # -----
    
    # ex2.py
    # Example of decorator
    
    def gg(xx):
        print "gg called"
        def s(y):
            return y-1
        return s
    
    
    @gg
    def ff(x):
        print "ff called"
        return x+1
    
    
    print ff(3)
    
    # -----
    
    # ex3.py
    # Check/Modify input argument
    
    def gg(func):
        """A decorator for ff. Make sure input to ff is always even, else, add
        1 to make it even."""
    
        def hh(y):
            if y % 2 ==0:
                return func(y)
            else:
                return func(y+1)
        return hh
    
    
    @gg
    def ff(x):
        return x
    
    print ff(3)
    print ff(2)
    print ff(9)
    
    # -----
    
    # ex4.py
    # Example of decorator that check condition to decide whether to call
    
    cc = True                       # change this to False to toggle
                                    # decorator action.
    
    def gg(func):                   # decorator
        """a decorator for ff. If cc is true, run ff, else do nothing."""
        def hh(*args, **kwargs):    # params must catch all args of ff
            """do nothing function"""
            pass
        if cc:
            return func
        else:
            return hh
    
    
    @gg
    def ff(*args, **kwargs):
        # ff can be sending email, or any callable with no return value
        print "ff"
        pass
    
    
    ff()    
    ff(3)
    ff(3, "jane")
    ff(3,4,k="thankyou")
    
    # -----
    
    # ex5.py
    # Decorator with parameter
    
    '''
    @g(3)
    def f():
        print("xyz")
    
    is equivaqlent to
    
    def f():
        print("xyz")
    
    f = g(3)(f)
    
    '''
    
    def gg(num):
        """a decorator for ff. Ignore ff. Simply return num."""
        def h1(f1):
            def h2(f2):
                return num
            return h2
        return h1
    
    # gg(1) must return a function h1, such that h1 accept function (the
    # ff), and also return a function (to be applied to ff's args))
    
    @gg(1)
    def ff(x):
        return repr(x) + " rabbits"
    
    print ff(3)
    print ff(4)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
