---
title: invert_array_index
date: 2020-05-07
---
Example Python program invert_array_index.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np

## Code

Python example

    # this is cool trick to invert array indices
    # basically the first becomes the last
    # and the last becomes the first
    
    arr = [1,2,3,4]
    arr_is = list(range(0, len(arr)))
    
    # iterate forwards
    for i in arr_is:
      print(arr[i])
      
    # iterate backwards!
    for i in arr_is:
      print(arr[~i])
      
    # the ~ operators performs an XOR on the number
    # thus flipping the number to the negative side
    # 0 becomes -1
    # 1 becomes -2
    # ...
    
    # this can be useful to select one of a pair and then the other of the pair
    
    # you can easily apply this to reverse numpy argsort
    import numpy as np
    for i in ~np.argsort(arr):
      print(arr[i])
    for i in np.argsort(arr):
      print(arr[~i])
    # which one is faster?
    # the above 2 or np.argsort(arr)[::-1]?
    # you be the judge! (probably not because [::-1] is a view)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
