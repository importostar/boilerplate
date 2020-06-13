---
title: range obj
date: 2020-05-07
---
Example Python program range-obj.py

## Modules

* from math import ceil

## Classes

* class Range(object):

## Methods

* def __init__(self, start, stop, step):
* def __repr__(self):
* def __len__(self):
* def __reversed__(self):
* def __getitem__(self, index):

## Code

Python example

    from math import ceil
    
    
    class Range(object):
    
        '''
        Range(start, stop, step) returns the arithmetic progression
        of numbers, whose lenght is ceil((stop - start) / step) and
        whose form [start, start + (step * 1), ..., start + (step *
        (len(obj) - 1)]. 
    
        Usage:
        >>> list(Range(0, 10, 3))
        [0, 3, 6, 9]
        >>> list(reversed(Range(0, 10, 3)))
        [9, 6, 3, 0]
        '''
    
        def __init__(self, start, stop, step):
    
            self.start = start
            self.stop = stop
            self.step = step
    
        def __repr__(self):
    
            return 'Range({0}, {1}, {2})'.format(self.start, self.stop, self.step)
    
        def __len__(self):
    
            return max(0, ceil((self.stop - self.start) / self.step))
    
        def __reversed__(self):
    
            return Range(self[-1], (self[0] - self.step), -self.step)
    
        def __getitem__(self, index):
    
            if not (-len(self) <= index < len(self)):
                raise IndexError('Index out of the range')
            return (self.start + (((len(self) + index) % len(self)) * self.step))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
