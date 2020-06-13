---
title: collections
date: 2020-05-07
---
Example Python program collections.py

## Modules

* from collections import deque

## Methods

* def odd_filter(n):
* def cube(n):

## Code

Python example

    # list aka sequence. array in other languages[]
    
    ints = [1,2,3,4,5]
    ints.append(6) # not push
    
    # set
    
    dupsList = [1,2,3,1,2,3]
    noDupSet = set(dupsList) #=> {1,2,3}
    
    # deque
    
    from collections import deque
    queue = deque(ints)
    
    queue.popleft() #=> 1
    queue.pop() #=> 5
    
    queue.append(6)
    
    # range
    
    range(1,10) #=> [1,2,3,4,5,6,7,8,9,10]
    
    # tuple
      # immutable
      # can be nested
    tup1 = 1,2,3 #=> (1,2,3)
    tup2 = tup1, #=> ((1,2,3), 4)
    
    # dictionary
    
    dict = {'x': 1, 'y': 2}
    
    # iterating
    names = ['adam', 'darcy', 'brian', 'alyssa']
    
    for i,v in enumerate(names):
      print i, ':', v
    
    #=> 0 : 'adam' 
    # and so on...
    
    for name in names:
      print name
    
    #=> adam
    # and so on
    
    for k,v in dict.iteritems():
      print k, ':', v 
      #=> 'x': 1
      #=> 'y': 2
    
    # functional programming
    
    def odd_filter(n):
      return n & 2 == 1
    
    filter(odd_filter, ints) #=> [1,3,5]
    
    def cube(n):
      return n * n * n
    
    map(cube, ints) #=> [1,8,27,64,125]
    
    # finding
    
    1 in dupList #=> True
    2 in noDupSet #=> True
    'q' in dict #=> False
    3 in tup1 #=> True

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
