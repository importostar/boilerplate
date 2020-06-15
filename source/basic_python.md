---
title: basic_python
date: 2020-05-07
---
Example Python program basic_python.py
For Python version 2.x.
To test your Python version use:

    python --version


## Methods

* def hello_world(name, times=3):
* def flex(*args, **kwargs):

## Code

Python example

    # Functions: indent blocks with 4 spaces
    def hello_world(name, times=3):
        print "Say", name*times
     
    hello_world("ni")
    
    # Data Types: 
    print [1, 2, "dog", True] # Lists
    print {1,1,2,3,5}         # Sets
    print {"Barca": 1, "Real Madrid": 2}
    
    # List indexing and slicing
    a = range(6)
    print a
    print a[2]        
    print a[1:2]      
    print a[:2]       
    print a[3:]       
    print a[-1]       
    print a[2:-2]     
    print a[-2:1:-1]  
    
    # List comprehension:
    [x**3 for x in a]
    
    [x**3 for x in a if x % 2 == 1]
    
    # Can also construct sets this way:
    word = "supercalifragilisticexpialidocious"
    {letter for letter in word} # Strings are sequences -> we can iterate over them
    
    # Or even dicts
    {letter: word.count(letter) for letter in word}
    
    # Loops are always loops over sequences:
    for item in ["eggs", "sugar", "milk"]:
        print "buy", item
    
    for index, item in enumerate(["eggs", "sugar", "milk"]):
        print "({number:02}) {stuff}".format(number=index, stuff=item)
    
    # Being clever:
    for v in enumerate(["eggs", "sugar", "milk"]):
        print "({}) {}".format(*v)
    In [68]:
    
    # More functions:
    def flex(*args, **kwargs):
        print ", ".join([str(arg) for arg in args]) # List comprehension: convert items to string
        for key in kwargs:
            print key, "=", kwargs[key]
        return 23, 42
     
    x, y = flex("hello", 99 ,dog="Bark")
    print x + 7
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
