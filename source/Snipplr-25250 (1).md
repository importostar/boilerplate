---
title: Snipplr 25250 (1)
date: 2020-05-07
---
Example Python program Snipplr-25250 (1).py


## Code

Python example

    ## Error handling in Python is done through the use of exceptions that are caught in try blocks and handled in except blocks. If an error is encountered, a TRy block code execution is stopped and transferred down to the except block, as shown in the following syntax:
    
    try:
        f = open(&quot;test.txt&quot;)
    except IOError:
        print &quot;Cannot open file.&quot;
    
    ## In addition to using an except block after the try block, you can also use the finally block. The code in the finally block will be executed regardless of whether an exception occurs.
    
    f = open(&quot;test.txt&quot;)
    try:
        f.write(data)
        . . .
    finally:
        f.close()
    
    ## You can raise an exception in your own program by using the raise exception [, value] statement. The value of exception is one of the built-in Python exceptions or a custom-defined exception object. The value of value is a Python object that you create to give details about the exception. Raising an exception breaks current code execution and returns the exception back until it is handled. The following example shows how to raise a generic RuntimeError exception with a simple text message value:
    raise RuntimeError, &quot;Error running script&quot;

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
