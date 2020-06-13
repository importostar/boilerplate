---
title: Snipplr 25248
date: 2020-05-07
---
Example Python program Snipplr-25248.py


## Code

Python example

    # The sys module provides an interface to access the environment of the Python interpreter.
    # The following examples illustrate some of the most common uses of the sys module.
    
    # The argv attribute of the sys module is a list. The first item in the argv list is the 
    # path to the module; the rest of the list is made up of arguments that were passed to the
    # module at the beginning of execution. The sample code shows how to use the argv list to 
    # access command-line parameters passed to a Python module:
    
    >>>print sys.argv
    ['C:\\books\\python\\CH1\\code\\print_it.py',
    'text']
    >>>print sys.argv[1]
    text
    
    # The stdin attribute of the sys module is a file object that gets created at the start of
    # code execution. In the following sample code, text is read from stdin (in this case, the
    # keyboard, which is the default) using the readline() function:
    
    >>>text = sys.stdin.readline()
    >>>print text
    Input Text
    
    # The sys module also has the stdout and stderr attributes that point to files used for
    # standard output and standard error output. These files default to writing to the screen.
    # The following sample code shows how to redirect the standard output and standard error 
    # messages to a file rather than to the screen:
    
    >>>sOUT = sys.stdout
    >>>sERR = sys.stderr
    >>>sys.stdout = open("ouput.txt", "w")
    >>>sys.stderr = sys.stdout
    >>>sys.stdout = sOUT
    >>>sys.stderr = sERR

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
