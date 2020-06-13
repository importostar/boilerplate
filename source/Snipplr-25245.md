---
title: Snipplr 25245
date: 2020-05-07
---
Example Python program Snipplr-25245.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import operator

## Code

Python example

    # build a dictionary that maps the ordinals from 32 to 255
    # to their ASCII character equivalents  eg. 33: '!'
    # (note that 32 and 160 are spaces)
    # Python24  by  vegaseat    10may2005
     
    import operator
     
    print &quot;ASCII values of characters:&quot;
    print '-'*27  # print 27 dashes, cosmetic
     
    # create an empty dictionary
    charD = {}
    # set keys from 32 to 255
    keyList = range(32, 256)
    # use map() to create the character list
    # applies function chr() to every item of the list
    valueList = map(chr, keyList)
    # use map() to form a dictionary from the two lists
    map(operator.setitem, [charD]*len(keyList), keyList, valueList)
     
    print &quot;%6s%6s%6s&quot; % (&quot;hex&quot;, &quot;dec&quot;, &quot;char&quot;)
    # print the dictionary one associated pair each line
    for key,value in charD.items():
        print &quot;%6x%6d%6c&quot; % (key, key, value)
     
    print '-'*27

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
