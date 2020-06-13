---
title: Hello_Python
date: 2020-05-07
---
Example Python program Hello_Python.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from time import sleep  #time for our program
* import webbrowser #web design
* import math #maths functions
* import string
* import random
* import time

## Classes

* class Shape:

## Methods

* def square(x,y): #functions for a square
* def minutes():
* def hours():
* def __init__(self, x, y):
* def area(self):

## Code

Python example

    from time import sleep  #time for our program
    import webbrowser #web design
    import math #maths functions
    import string
    import random
    import time
    
    def square(x,y): #functions for a square
        return x*y
    
    
    list(string.ascii_lowercase)
    
    print (string.ascii_lowercase[12:18])
    
    print(random.choice(foo))
    
    alphabetletters = string.ascii_lowercase
    
    webbrowser.open_new_tab("google.com")
    
    
    print("Welcome to the Python Atomic Clock") #Welcome to the Python Atomic Clock
    sleep(3)
    hello=("Hello") #Strings
    sleep(3)
    print(hello) #print: Hello
    sleep(3)
    
    mynewlist = ["Yes", "No", "Maybe"]
    
    print(mynewlist) #Print the Whole List
    print(mynewlist[1:3]) #Print a section
    
    for x in range(1,20):  #prints a timer
        print(x)
        sleep(1)
    
    
    
    square(2,4)
    
    while True:
        
        yes=input("Type NOW!")
    
        if yes == "no" or yes == "yes":
            print("Confusion-")
    
        elif yes != "yes" and yes != "no":
            print(".")
    
        else:
            break
          
    time_minutes = 0
    time_hours = 0
    
    
    def minutes():
    
        while True:
    
            sleep(60)
            time_minutes = time_minutes + 1
    
    
    def hours():
    
        while True:
    
            sleep(3600)
            time_hours = time_hours + 1
    
    
    hours()
    minutes()
    
    
    class Shape:
    
        def __init__(self, x, y):
            self.x = 6
            self.y = 6
    
        def area(self):
            return self.x * self.y

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
