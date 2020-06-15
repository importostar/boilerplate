---
title: Python_arithmatic_operators_Arthmatic_Operator
date: 2020-05-07
---
Example Python program Python_arithmatic_operators_Arthmatic_Operator.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    x = 50
    print(x)
    print(x / 8)  # returns the floating fomat value
    print(x // 8)  # returns the round of int value
    x += 10
    print(x)  # increasing 10 of x value
    y = 10
    print(y ** 2)  # returns the value of y to power 2 i.e in java pow(y,2)
    
    # ------------- Operator Precedence --------------------
    
    # in operator precedence :
    # 1: parenthesis ()
    # 2:first power will come i.e (2**5) here
    # 3:then * and / being same precedence value , so whatever will come first from left to right that
    # will be evaluated first i.e (2*5) here
    # 4:then comes / i.e 10/3
    # 5: then comes +  or - as usual
    result = 50 + 2 * 5 / 3 - 2 ** 5
    print(result)  # so here it returns
    # 50+2*5/3-32
    # 50+10/3-32
    # 50+3.33-32
    # 53.33-32
    # 21.33
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
