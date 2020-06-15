---
title: Snipplr 25261
date: 2020-05-07
---
Example Python program Snipplr-25261.py


## Code

Python example

    ## The first example uses a string as the sequence to create a list of characters in the string:
    
    >>>word = "Python"
    >>>list = []
    >>>for ch in word:
    >>>    list.append(ch)
    >>>print list
    ['P', 'y', 't', 'h', 'o', 'n']
    
    
    ## This example uses the range() function to create a temporary sequence of integers the size of a list so the items in the list can be added to a string in order:
    
    >>>string = ""
    >>>for i in range(len(list)):
    >>>    string += list[i]
    >>>print string
    Python
    
    
    
    ## This example uses the enumerate(string) function to create a temporary sequence. The enumerate function returns the enumeration in the form of (0, s[0]), (1, s[1]), and so on, until the end of the sequence string, so the for loop can assign both the i and ch value for each iteration to create a dictionary:
    
    >>>dict = {}
    >>>for i,ch in enumerate(string):
    >>>    dict[i] = ch
    >>>print dict
    {0: 'P', 1: 'y', 2: 't', 3: 'h', 4: 'o', 5: 'n'}
    
    
    
    ## This example uses a dictionary as the sequence to display the dictionary contents:
    
    >>>for key in dict:
    >>>    print key, '=', dict[key]
    0 = P
    1 = y
    2 = t
    3 = h
    4 = o
    5 = n

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
