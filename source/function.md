---
title: function
date: 2020-05-07
---
Example Python program function.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def my_function():
* def my_func ():
* def my_func(country = "India"):
* def func_one(vegetables = "potato"):
* def my_func(x):
* def myfunc(n):
* def absolute_number(num):
* def avg_num(x,y):
* def multiple_value(x,y,z):
* def square_sum(x,y):
* def printme( str ):
* def changeme(mylist):

## Code

Python example

    c:\any\dir> spyder --reset
    #%reset -f
    #%%
    #091 Functions in Python
    #Creation
    def my_function():
        print("Hello")
    #created a new function,how to call the function?
    my_function()
    #Write a function and return the value of variable of the function
    def my_func ():
        x = 10
        print("value inside the function :", x)
    y = 20
    my_func()
    print("value is outside the function :", y)    
    #how to pass default value to the function
    def my_func(country = "India"):
        print("I am from " + country)
    my_func("India")
    #
    def func_one(vegetables = "potato"):
        print("i am fond of" + vegetables)
    func_one( "Carrot")
    #how to write a function that Returns Values
    def my_func(x):
        return 5 * x
    print(my_func(3))
    #lambda functions
    #create a function that gives square,cubes etc of integers
    myfunc = lambda i : i**2
    print(myfunc(3))
    #
    myfunc = lambda i : i**4
    print(myfunc(5))
    #
    myfunc = lambda i : i**3
    print(myfunc(6))
    #
    myfunc = lambda i: i**5
    print(myfunc(2))
    #create a function that multiplies two integers
    myfunc = lambda x,y : x*y
    print(myfunc(5,6))
    #create a function which creates an anonymous function #that multiplies 
    #variable i with variable n.
    def myfunc(n):
        return lambda i : i*n
    double = myfunc(2)
    triple = myfunc(3)
    val = 11
    print ("Double: " + str(double(val)) + "Triple: " + str(triple(val)))
    # Write a function that returns the absolute number
    def absolute_number(num):
        if num >= 0:
            return num
        else:
            return -num
    print(absolute_number(4))
    print(absolute_number(-4))
    #Write a function that gives the average of two numbers.
    #always the return need to be outside the function.
    def avg_num(x,y):
        print("Average of ",x, "and", y,"is ",(x+y)/2)
    avg_num(3,4)
    #Write a function that returns the multple of three numbers
    def multiple_value(x,y,z):
        print("The expected value of", x,y,z,"is", x*y*z)
    multiple_value(7,8,9)
    #Write a function that returns the square of sum of two values.
    def square_sum(x,y):
        return(x*x+2*x*y+y*y)
        print("The square of sum of 2 and 3 is :", square_sum(2,3))
    square_sum(8,9)
    #
    def printme( str ):
       "This prints a passed string into this function"
       print(str)
       return;
    printme("Outside is cloudy")
    #
    def changeme(mylist):
        "This change is passed to the function"
        mylist.append([1,2,3,4,5,6])
        print("Values inside the function: ", mylist)
        return
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
