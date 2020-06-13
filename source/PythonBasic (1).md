---
title: PythonBasic (1)
date: 2020-05-07
---
Example Python program PythonBasic (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    # Vars (auto typing)
    lastname = "someLastName"
    name ="someName"
    
    # Upper / lower
    upper = language.upper()
    lower = language.lower()
    # Concat
    fullname = name + " " + lastname
    
    # Array
    items = ['laptop','phone','joystick']
    
    # Array destructuring
    laptop, phone, joystick = items
    laptop, *other = items
    print(other)
    
    # Array push to
    items.append('nex item at the end')
    items.insert(0, "at index 0")
    
    # Array remove
    items.pop()  
    
    # MultiSentence
    """
    Multiline sentence
    Hehe 
    """"
    
    # Add quote
    greeting = "Ed once said \"magic is dead\""
    
    # Sugar syntax
    welcome = " Hello there { lastname } { name }and nevermind" 
    
    # length
    print(len(welcome))
    
    # Access individual letter
    letter = name[0] // s
    letterRange = name[0:3] // som
    rangetoEnd = name[1:]
    range to start = name[:4]
    negative = name[-1] // last letter from end

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
