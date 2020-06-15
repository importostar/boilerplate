---
title: python_basics
date: 2020-05-07
---
Example Python program python_basics.py
For Python version 2.x.
To test your Python version use:

    python --version


## Classes

* class Dog:

## Methods

* def myFunc():
* def myPlus(x, y):
*    def __init__(self, age):
*    def printAge(self):

## Code

Python example

    #!/usr/bin/python
    
    print "Hello"
    
    # If
    # Code blocks are differentiated by their indentation
    # Complex statements, such as "if" require header line, which ends with colon (:)
    if True:
       print "Answer"
       print "True"
    else:
       print "Answer"
       print "False"
    
    # This is how to wair for user input
    raw_input("\n\nPress the enter key to exit.")
    
    # Variables
    x = 10
    print x
    x = "dsfdsf"
    print x
    
    # We can delete object references
    del x
    # This will throw exception
    # print x
    
    # Type conversion
    x = 5	# x is int
    y = float(5)	# y is float
    print y
    
    # Ifs can be one line
    if (x == 5) : print "x is 5"
    
    # Functions
    def myFunc():
    	print "My Function"
    	return
    
    myFunc()
    
    def myPlus(x, y):
    	return x + y
    
    print myPlus(1, 5)
    
    # Classes
    class Dog:
       # This is class variable (like static in Java)
       # This is referenced ad Dog.counter
       counter = 0
     
       # This is constructor
       def __init__(self, age):
       	  # Here we access instance variable
          self.age = age
    
       def printAge(self):
          print self.age
    
    dog = Dog(5)
    dog2 = Dog(10)
    
    dog.printAge()	# result is 5
    dog2.printAge()	# result is 10
    
    print Dog.counter 	# result is 0
    
    Dog.counter = 123
    print Dog.counter
    print dog.counter
    print dog2.counter
    # result is all the same 123, because all class instances share the same class variable

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
