---
title: python string shorthand
date: 2020-05-07
---
Example Python program python-string-shorthand.py
For Python version 2.x.
To test your Python version use:

    python --version


## Code

Python example

    Python has hidden shorthands to make your life significantly easier. To reverse a string, we simply add ::-1 as list indices
    
    >>> a =  "ilovepython" 
    >>> print a[::-1] 
    nohtypevoli
    
    The same trick can be applied to a list of integers as well. String manipulation is extremely easy in Python. For example, if you want to output a sentence using the following predefined variables str1 , str2 and lst3
    
    >>> str1 = "Totally"
    >>> str2 = "Awesome"
    >>> lst3 = ["Omg", "You", "Are"]
    
    Simply use the .join() method and arithmetic operators to create the desired sentence.
    
    >>> print ' '.join(lst3)
    Omg You Are
    >>> print ' '.join(lst3)+' '+str1+' '+str2
    Omg You Are Totally Awesome

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
