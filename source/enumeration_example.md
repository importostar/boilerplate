---
title: enumeration_example
date: 2020-05-07
---
Example Python program enumeration_example.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    >>> # Suppose we have this list of tuples, each of length two.
    ... # Element 1 is a persons first name, element 2 is their last name
    ...
    >>> names = [('Joseph', 'McCullough'), ('Luke', 'PolishLastName')]
    >>> # Now, if we do a normal for loop, the item per each iteration is
    ... # a tuple
    ...
    >>> for name in names:
    ...     print("first: " + name[0])
    ...     print("last: " + name[1])
    ...
    first: Joseph
    last: McCullough
    first: Luke
    last: PolishLastName
    >>> # First, let's look at tuple assignment. You can order-wise assign elements
    ... # of a tuple to variables
    ...
    >>> joseph = names[0]
    >>> joseph
    ('Joseph', 'McCullough')
    >>> first,last = joseph
    >>> first
    'Joseph'
    >>> last
    'McCullough'
    >>> # Because of this, when we set up our foor loop, we can do the same
    ...
    >>> for first,last in names:
    ...     print("first: " + first)
    ...     print("last: " + last)
    ...
    first: Joseph
    last: McCullough
    first: Luke
    last: PolishLastName
    >>> # Let's take a look at what enumerate does. It's a function you call on a list
    ...
    >>> mylist = ['cat', 'dog', 'fish', 'thing']
    >>> list(enumerate(mylist))
    [(0, 'cat'), (1, 'dog'), (2, 'fish'), (3, 'thing')]
    >>> # So you see it takes each element of the list, makes a 2-length tuple with
    ... # the first element the index of the element, and second element the value
    ... # So now we have what we need to iterate over a list and keep track of its index
    ...
    >>> for i,animal in enumerate(mylist):
    ...     print("The animal: " + animal)
    ...     print("The index: " + str(i))
    ...
    The animal: cat
    The index: 0
    The animal: dog
    The index: 1
    The animal: fish
    The index: 2
    The animal: thing
    The index: 3
    >>> # The main use case of using enumerate like this is to alter list elements
    ... # during iteration. Observe that through a normal loop, we cannot alter
    ... # the elements outside of the loop body
    ...
    >>> mylist
    ['cat', 'dog', 'fish', 'thing']
    >>> for animal in mylist:
    ...     animal = "LOL"
    ...
    >>> mylist
    ['cat', 'dog', 'fish', 'thing']
    >>> # But, by referencing the element through list indexing, we can change the
    ... # element
    ...
    >>> for i, animal in enumerate(mylist):
    ...     mylist[i] = animal + "hahahah"
    ...
    >>> mylist
    ['cathahahah', 'doghahahah', 'fishhahahah', 'thinghahahah']

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
