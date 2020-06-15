---
title: Collect.Counter (1)
date: 2020-05-07
---
Example Python program Collect.Counter (1).py

## Modules

* import re

## Code

Python example

    ############
    # Tally occurrences of words in a list
    cnt = Counter()
    for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
        cnt[word] += 1
    cnt
    #Counter({'blue': 3, 'red': 2, 'green': 1})
    
    ############
    # Find the ten most common words in Hamlet
    import re
    words = re.findall(r'\w+', open('hamlet.txt').read().lower())
    Counter(words).most_common(10)
    
    #[('the', 1143), ('and', 966), ('to', 762), ('of', 669), ('i', 631),
     ('you', 554),  ('a', 546), ('my', 514), ('hamlet', 471), ('in', 451)]
     
    ############
    # Initialize Counters
    >>> c = Counter()                           # a new, empty counter
    >>> c = Counter('gallahad')                 # a new counter from an iterable
    >>> c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
    >>> c = Counter(cats=4, dogs=8)             # a new counter from keyword args
    
    # Calling on Elements
    >>> c = Counter(['eggs', 'ham'])
    >>> c['bacon']                              # count of a missing element is zero
    # 0
    
    # Counter entry with zero count
    >>> c['sausage'] = 0                        # counter entry with a zero count
    >>> del c['sausage']                        # del actually removes the entry
    
    ########
    # elements() method
    # Return an iterator over elements repeating each 
    # as many times as its count. Elements are returned 
    # in arbitrary order. If an element’s count is less 
    # than one, elements() will ignore it.
    
    c = Counter(a=4, b=2, c=0, d=-2)
    list(c.elements())
    #['a', 'a', 'a', 'a', 'b', 'b']
    
    ########
    # most_common([n]) method
    # Return a list of the n most common elements and their 
    # counts from the most common to the least. If n is omitted 
    # or None, most_common() returns all elements in the counter. 
    # Elements with equal counts are ordered arbitrarily:
    
    Counter('abracadabra').most_common(3)
    #[('a', 5), ('r', 2), ('b', 2)]
    
    ########
    # subtract([iterable-or-mapping])
    # Elements are subtracted from an iterable or from another 
    # mapping (or counter). Like dict.update() but subtracts counts 
    # instead of replacing them. Both inputs and outputs may be 
    # zero or negative.
    
    c = Counter(a=4, b=2, c=0, d=-2)
    d = Counter(a=1, b=2, c=3, d=4)
    c.subtract(d)
    c
    #Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
    
    
    #########
    #The usual dictionary methods are available for Counter objects except for two which 
    #work differently for counters.
    
    #fromkeys(iterable)
    #This class method is not implemented for Counter objects.
    
    ##########
    #update([iterable-or-mapping])
    #Elements are counted from an iterable or added-in from another mapping (or counter).
    #Like dict.update() but adds counts instead of replacing them. Also, the iterable is 
    #expected to be a sequence of elements, not a sequence of (key, value) pairs.
    
    
    ##########
    # Common patterns for working with Counter objects:
    
    sum(c.values())                 # total of all counts
    c.clear()                       # reset all counts
    list(c)                         # list unique elements
    set(c)                          # convert to a set
    dict(c)                         # convert to a regular dictionary
    c.items()                       # convert to a list of (elem, cnt) pairs
    Counter(dict(list_of_pairs))    # convert from a list of (elem, cnt) pairs
    c.most_common()[:-n-1:-1]       # n least common elements
    c += Counter()                  # remove zero and negative counts
    
    # Several mathematical operations are provided for combining Counter objects 
    # to produce multisets (counters that have counts greater than zero). Addition 
    # and subtraction combine counters by adding or subtracting the counts of 
    # corresponding elements. Intersection and union return the minimum and maximum 
    # of corresponding counts. Each operation can accept inputs with signed counts, 
    # but the output will exclude results with counts of zero or less.
    
    >>> c = Counter(a=3, b=1)
    >>> d = Counter(a=1, b=2)
    >>> c + d                       # add two counters together:  c[x] + d[x]
    Counter({'a': 4, 'b': 3})
    >>> c - d                       # subtract (keeping only positive counts)
    Counter({'a': 2})
    >>> c & d                       # intersection:  min(c[x], d[x])
    Counter({'a': 1, 'b': 1})
    >>> c | d                       # union:  max(c[x], d[x])
    Counter({'a': 3, 'b': 2})
    
    
    
    
    
    
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
