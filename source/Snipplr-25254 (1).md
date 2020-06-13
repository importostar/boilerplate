---
title: Snipplr 25254 (1)
date: 2020-05-07
---
Example Python program Snipplr-25254 (1).py
For Python version 2.x.
To test your Python version use:

    python --version


## Methods

* To create a function, use the def functionname(parameters): statement, and then define the function in the following code block. Once the function has been defined, you can call it by specifying the function name and passing the appropriate parameters.
* def fun(name, location, year=2006):

## Code

Python example

    ## Functions are objects in the Python language and the parameters that are passed are really "applied" to the function object.
    To create a function, use the def functionname(parameters): statement, and then define the function in the following code block. Once the function has been defined, you can call it by specifying the function name and passing the appropriate parameters.
    
    def fun(name, location, year=2006):
        print "%s/%s/%d" % (name, location, year)
    
    
    ## The first example shows the function being called by passing the parameter values in order. Notice that the year parameter has a default value set in the function definition, which means that this parameter can be omitted and the default value will be used.
    
    >>>fun("Teag", "San Diego")
    Teag/San Diego/2006
    
    ## The next example shows passing the parameters by name. The advantage of passing parameters by name is that the order in which they appear in the parameter list does not matter.
    
    >>>fun(location="L.A.", year=2004, name="Caleb" )
    Caleb/L.A./2004
    
    ## This example illustrates the ability to mix different methods of passing the parameters. In the example, the first parameter is passed as a value, and the second and third are passed as an assignment.
    
    >>>fun("Aedan", year=2005, location="London")
    Aedan/London/2005
    
    ## Parameters can also be passed as a tuple using the * syntax, as shown in this example. The items in the tuple must match the parameters that are expected by the function.
    
    >>>tuple = ("DaNae", "Paris", 2003)
    >>>fun(*tuple)
    DaNae/Paris/2003
    
    ## Parameters can also be passed as a dictionary using the ** syntax, as shown in this example. The entries in the dictionary must match the parameters that are expected by the function.
    
    >>>dictionary = {'name':'Brendan',
    'location':'Orlando', 'year':1999}
    >>>fun(**dictionary)
    Brendan/Orlando/1999

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
