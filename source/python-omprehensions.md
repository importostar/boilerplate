---
title: python omprehensions
date: 2020-05-07
---
Example Python program python-omprehensions.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    # Use this as a template for list - single line for loop.
    
    new_list = [x for x in some_list]
    
    
    # Doubling every item in a list
    some_list = [1,2,3,4]
    new_list = [x * 2 for x in some_list]
    print(new_list)
    
    # Doubling every item in a list that is larger than 2
    some_list = [1,2,3,4]
    new_list = [x * 2 for x in some_list if x > 2]
    print(new_list)
    
    
    # Use this as a template for Dictionary
    
    d = {'a':1,'b':2,'c':3}
    for pair in d.items():
      print(pair)
    
    d = {k:v for (k,v) in d.items()}
    
    # Creating a new dictionary with only pairs where the value is larger than 2
    d = {'a':1,'b':2,'c':3}
    d = {k:v for (k,v) in d.items() if v > 2}
    print(d)
    
    
    # We can also perform operations on the key value pairs
    d = {'a':1,'b':2,'c':3}
    d = {k + 'c':v * 2 for (k,v) in d.items() if v > 2}
    print(d)
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
