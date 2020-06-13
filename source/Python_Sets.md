---
title: Python_Sets
date: 2020-05-07
---
Example Python program Python_Sets.py


## Code

Python example

    >>> A = {1, 2, 5, 4, 7, 9, 2}
    >>> A
    {1, 2, 4, 5, 7, 9}
    >>> len(A)
    6
    >>> A.add(10)
    >>> A
    {1, 2, 4, 5, 7, 9, 10}
    >>> A.add(10)
    >>> A
    {1, 2, 4, 5, 7, 9, 10}
    >>> A.update([15, 18, 17, 14])
    >>> A
    {1, 2, 4, 5, 7, 9, 10, 14, 15, 17, 18}
    >>> A.remove(18)
    >>> A
    {1, 2, 4, 5, 7, 9, 10, 14, 15, 17}
    >>> A.discard(17)
    >>> A
    {1, 2, 4, 5, 7, 9, 10, 14, 15}
    >>> A.remove(100)
    Traceback (most recent call last):
      File "<input>", line 1, in <module>
    KeyError: 100
    >>> A.discard(100)
    >>> A.pop()
    1
    >>> name = {'max', 'tom', 'Den'}
    >>> name.clear()
    >>> name
    set()
    >>> del name
    >>> name
    Traceback (most recent call last):
      File "<input>", line 1, in <module>
    NameError: name 'name' is not defined
    >>> name = set(('max', 'tom', 'Den'))
    >>> name
    {'tom', 'max', 'Den'}
    >>> Z = set([1,2,3,5])
    >>> Z
    {1, 2, 3, 5}
    >>> A
    {2, 4, 5, 7, 9, 10, 14, 15}
    >>> B = {10, 11, 12, 13, 14, 16, 18}
    >>> A | B
    {2, 4, 5, 7, 9, 10, 11, 12, 13, 14, 15, 16, 18}
    >>> A.union(B)
    {2, 4, 5, 7, 9, 10, 11, 12, 13, 14, 15, 16, 18}
    >>> A & B
    {10, 14}
    >>> A.intersection(B)
    {10, 14}
    >>> A - B
    {2, 4, 5, 7, 9, 15}
    >>> B - A
    {16, 18, 11, 12, 13}
    >>> A.difference(B)
    {2, 4, 5, 7, 9, 15}
    >>> B.difference(A)
    {16, 18, 11, 12, 13}
    >>> A ^ B
    {2, 4, 5, 7, 9, 11, 12, 13, 15, 16, 18}
    >>> B  ^ A
    {2, 4, 5, 7, 9, 11, 12, 13, 15, 16, 18}
    >>> A.symmetric_difference(B)
    {2, 4, 5, 7, 9, 11, 12, 13, 15, 16, 18}
    >>> A[0]
    Traceback (most recent call last):
      File "<input>", line 1, in <module>
    TypeError: 'set' object does not support indexing
    >>> dir (A)
    ['__and__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__iand__', '__init__', '__ior__', '__isub__', '__iter__', '__ixor__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__or__', '__rand__', '__reduce__', '__reduce_ex__', '__repr__', '__ror__', '__rsub__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__xor__', 'add', 'clear', 'copy', 'difference', 'difference_update', 'discard', 'intersection', 'intersection_update', 'isdisjoint', 'issubset', 'issuperset', 'pop', 'remove', 'symmetric_difference', 'symmetric_difference_update', 'union', 'update']
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
