---
title: Dictionary (1)
date: 2020-05-07
---
Example Python program Dictionary (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    #Dictionary in Python is an unordered collection of data values, used to store data values like a map, which unlike other Data Types that hold only single value as an element, Dictionary holds key:value pair.
    
    dict1 = {} #empty dictionary
    
    dict1 = {1:"value1", "key1":"value2", 2:"value3"}
    
    print(dict1) #{1: 'value1', 'key1': 'value2', 2: 'value3'}
    print(dict1["key1"]) #value2
    print(dict1[1]) #value1
    
    #keys
    print(dict1.keys()) #dict_keys([1, 'key1', 2])
    for item in dict1.keys():
        print("{0} likes the value {1}.".format(item, dict1[item]))
    '''
    1 likes the value value1.
    key1 likes the value value2.
    2 likes the value value3.
    '''
    
    #Keys cannot be changed.
    #You will need to add a new key with the modified value then remove the old one.
    
    #modifing
    dict1[2]="name3"
    print(Dict1) #{1: 'value1', 'key1': 'value2', 2: 'name3'}
    
    #adding
    dict1.update({125:"value125"})
    print(dict1) #{1: 'value1', 'key1': 'value2', 2: 'name3', 125: 'value125'}
    
    #deleting
    del dict1[1]
    print(dict1) #{'key1': 'value2', 2: 'name3', 125: 'value125'}
    
    #counting
    print(len(dict1)) #3
    
    #clearing
    dict1.clear()
    print(len(dict1)) #0

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
