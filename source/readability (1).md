---
title: readability (1)
date: 2020-05-07
---
Example Python program readability (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from cs50 import get_string

## Code

Python example

    from cs50 import get_string
    
    text = get_string("Text :")
    letters = 0
    words = 1
    sentences = 0
    for i in range(len(text)):
        if text[i] == " ":
            words += 1
        if text[i] == "." or text[i] == "!" or text[i] == "?":
            sentences += 1
        if text[i].isalpha():
            letters += 1
    
    
    l = (letters / words) * 100
    s = (sentences / words) * 100
    index = (0.0588 * l) - (0.296 * s) - 15.8
    i = round(index)
    if index < 1:
        print("Before Grade 1")
    elif index >= 1 and index < 16:
        print("Grade ", i)
    else:
        print("Grade 16+")
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
