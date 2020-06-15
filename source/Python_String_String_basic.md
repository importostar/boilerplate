---
title: Python_String_String_basic
date: 2020-05-07
---
Example Python program Python_String_String_basic.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    message = 'hello python programmers'
    print(message)
    
    # multiline string
    text = '''Hello Python programmers
            what are u guys doing now ?
            can anyone suggest me what will be best framework for 
            python web application development'''
    print(text)
    # the length of the String can be calculated as len() provided by python
    
    # here we can consatinate the String with the number or int type either by formatting
    # or by converting the context into String type by the str(arg) method provided bby python
    print('the length of the first string is : {}'.format(len(message)))
    # or
    print('the length of the string is ' + str(len(text)))
    # in python a string is treated as an array of the characters like string[index]
    # type of the string[index] is also the String
    print(type(message[0]))  # returns the first character of the string
    print(message[-1])  # returns the last character of the String
    print(text[-5])  # returns the 5th from last of the String
    
    # we can also mention the range of indexes like as
    print(text[5:10])  # here it always includes the starting element ad excludes the ending element
    # if the starting index is not given then it considers from zero (0) as starting point. so here it considers
    # from zero to 15 th element by excluding 15th element
    print(text[:15])
    # exactly like if the the end point is not mentioned , then bydefault it considers
    # the last element as the last element
    print(message[5:])  # returns the string from 5th element to the last element
    
    name = 'Aurobinda Moharana'
    print(name[2:-2])  # returns the substring containning from index 2 to the second last element
    # i.e -----robinda Mohara
    
    # -----------methods of the String in python----------
    
    print(name.upper())  # returns string uppercase letter
    print(name.lower())  # returns string in lowercase letter
    print(name.find('b'))  # it will return index of the first occurance of the  String, if not found return -1
    print(name.replace('aurobinda', 'Abhimanyu'))  # replace the second string with old string if not found ,
    # returns the old string
    print(name.replace('A', 'anshuraj'))  # also we can replace one large String instead of a single character
    print('Moharana' in name)  # finds and return a boolean True if found or else returns False
    # or we also can write like this
    str = input('enter ur orginal string \n')
    serch_str = input('enter the String u want to search \n')
    # so basically find and in methods acts like same way but results diffrently, in method returns boolean
    # while find method returns their indes value
    print(serch_str in str)
    print(str.find(serch_str))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
