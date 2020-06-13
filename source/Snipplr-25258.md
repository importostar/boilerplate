---
title: Snipplr 25258
date: 2020-05-07
---
Example Python program Snipplr-25258.py


## Methods

* >>>def a(s):
* >>>def switch(ch):

## Code

Python example

    ## There is currently no switch statement in Python. Often this is not a problem and can be handled through a series of if-elif-else statements. However, there are many other ways to handle the deficiency. The following example shows how to create a simple switch statement in Python:
    
    >>>def a(s):
    >>>    print s
    >>>def switch(ch):
    >>>    try:
    >>>      {'1': lambda : a("one"),
    >>>       '2': lambda : a("two"),
    >>>       '3': lambda : a("three"),
    >>>       'a': lambda : a("Letter a")
    >>>      }[ch]()
    >>>    except KeyError:
    >>>      a("Key not Found")
    >>>switch('1')
    one
    >>>switch('a')
    Letter a
    >>>switch('b')
    Key not Found
    
    
    ## Remember that we are making use of the following method for checking the existence of a Key...:
    
    >>> {1: 2}[1]
    >>> 2
    >>> {1: 2}[0]
    Key Error......
    
    
    ## p.s. check also the entry about the use of lambda in a dictionary...

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
