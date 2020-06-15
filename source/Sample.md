---
title: Sample
date: 2020-05-07
---
Example Python program Sample.py

## Modules

* import unittest

## Methods

* def my_function(x, y):

## Code

Python example

    x = 34 - 23 # A comment.
    
    y = "Hello" # Another one.
    
    z = 3.45
    
    if z == 3.45 or y == “Hello”:
        x = x + 1
        y = y + "World" # String concat.
    
    print x
    print y
    
    def my_function(x, y):
    """This is the docstring. This
    function does blah blah blah."""
    # The code would go here...
    
    a = [1, 2, 3]
    
    b = a
    
    a.append(4)
    
    tuple = (23, 'abc', 4.56, (2, 3), 'def')
    tuple[1:4]
    
    import unittest
    
    class UnitTests02(unittest.TestCase):
        def testFoo(self):
            self.failUnless(False)
        def checkBar01(self):
            self.failUnless(False)
    
    class UnitTests01(unittest.TestCase):
        # Note 1
        def setUp(self):
            print 'setting up UnitTests01'
        def tearDown(self):
            print 'tearing down UnitTests01'
        def testBar01(self):
            print 'testing testBar01'
            self.failUnless(False)
        def testBar02(self):
            print 'testing testBar02'
            self.failUnless(False)
    
    def function_test_1():
        name = 'mona'
        assert not name.startswith('mo')
    def compare_names(name1, name2):
        if name1 < name2:
            return 1
        elif name1 > name2:
            return ­1
        else:
            return 0
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
