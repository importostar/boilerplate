---
title: generate_grid (1)
date: 2020-05-07
---
Example Python program generate_grid (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random

## Methods

* def get_int(msg,minimum,default):

## Code

Python example

    #!/usr/bin/env python
    # coding: utf-8
    import random
    
    def get_int(msg,minimum,default):
        while True:
            try:
                line = input(msg)
                if not line and default is not None:
                    return default
                i = int(line)
                if i < minimum:
                    print ("must be >=" , minimum)
                else:
                    return i
            except ValueError as err:
                print(err)
    
    rows = get_int("rows: ", 1, None)
    columns = get_int("columns: ",1,None)
    minimum = get_int("minimum (or enter for 0): ",-1000000,0)
    
    default = 1000
    if default < minimum:
        default = 2 * minimum
    maximum = get_int("maximum (or Enter for " + str(default)+"):",minimum,default)
    
    
    row = 0
    while row < rows:
        line = ""
        column = 0
        while column < columns:
            i=random.randint(minimum,maximum)
            s = str(i)
            while len(s) < 10:
                s=" "+s
            line +=s
            column +=1
        print(line)
        row+=1
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
