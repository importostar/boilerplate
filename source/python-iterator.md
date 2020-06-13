---
title: python iterator
date: 2020-05-07
---
Example Python program python-iterator.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class NewNumbers:

## Methods

* def __iter__(self):
* def __next__(self):

## Code

Python example

    # __iter__() returns the iterator object
    # __next__() returns the next item in the sequence
    
    
    # creating a list
    new_list = [1, 2, 3, 7, 9]
    
    # using iter()
    new_iter = iter(new_list)
    
    # print 1
    print(next(new_iter))
    
    # print 2
    print(next(new_iter))
    
    # print 3
    print(new_iter.__next__())
    
    # print 7
    print(new_iter.__next__())
    
    # print 9
    print(new_iter.__next__())
    
    # looping thru new_list
    for element in new_list:
        print(element)
        
    # build an iterator
    class NewNumbers:
        def __iter__(self):
            self.a = 1
            return self
        
        def __next__(self):
            x = self.a
            self.a += 1
            return x
        
    newclass = NewNumbers()
    newiter = iter(newclass)
    
    #print the iteration
    print(next(newiter))
    print(next(newiter))
    print(next(newiter))
    print(next(newiter))
    print(next(newiter))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
