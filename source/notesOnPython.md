---
title: notesOnPython
date: 2020-05-07
---
Example Python program notesOnPython.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from datetime import datetime

## Methods

* def foo(bar=[]):# bar is optional and defaults to [] if not specified
* def reverse(text):
* def anti_vowel(text):

## Code

Python example

    def foo(bar=[]):        # bar is optional and defaults to [] if not specified
    ...    bar.append("baz")    # but this line could be problematic, as we'll see...
    ...    return bar
    #=========
    print dir(math)
    print type(2.)
    
    duck_index =animals.index("duck")    # Use index() to find "duck"
    animals = animals.insert(duck_index,"cobra")
    square_list.sort()
    // =======
    from datetime import datetime
    now = datetime.now()
    print '%s/%s/%s' % (now.month, now.day, now.year)
    print '%s:%s:%s' % (now.hour, now.minute, now.second)
    // =======
    for i in range(0,10):
        print random.randint(0,2)
    // =======
    for a,b in zip(a,b):
        print a+b
    // =======
    for index,a  in enumerate(a):
    print index,a
    // =======
    def reverse(text):
        temp = ""
        for i in range(len(text)-1,-1,-1):
            temp =temp + text[i]
        return temp
    // =======
    def anti_vowel(text):
        text= list(text)
        for c in range(0,len(text)):
            if text[c] in  "aeiouAEIOU":
                text[c] = ""
        return   ''.join(text)
    print anti_vowel("abce")
    // =======
    sorted([6, 8, 12, 2, 23])
    my_string.count("d")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
