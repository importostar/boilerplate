---
title: Snipplr 25255
date: 2020-05-07
---
Example Python program Snipplr-25255.py

## Modules

* ## Modules can be imported directly using the package or module name. Items in submodules must be accessed explicitly including the full package name.
* >>> import os
* ## Modules can be imported directly using the module name, but the namespace should be named something different. Items in submodules must be accessed explicitly including the full package name:
* >>> import os as computer
* ## Modules can be imported using the module name within the package name. Items in submodules must be accessed explicitly including the full package name:
* >>> import os.path
* ## Modules can be imported by importing the modules specifically from the package. Items in submodules can be accessed implicitly without the package name:
* >>> from os import path

## Code

Python example

    ## Modules can be imported directly using the package or module name. Items in submodules must be accessed explicitly including the full package name.
    
    >>> import os
    >>> os.path.abspath(".")
    'C:\\books\\python'
    
    
    ## Modules can be imported directly using the module name, but the namespace should be named something different. Items in submodules must be accessed explicitly including the full package name:
    
    >>> import os as computer
    >>> computer.path.abspath(".")
    'C:\\books\\python'
    
    
    ## Modules can be imported using the module name within the package name. Items in submodules must be accessed explicitly including the full package name:
    
    >>> import os.path
    >>> os.path.abspath(".")
    'C:\\books\\python'
    
    
    ## Modules can be imported by importing the modules specifically from the package. Items in submodules can be accessed implicitly without the package name:
    
    >>> from os import path
    >>> path.abspath(".")
    'C:\\books\\python'
    
    
    ## Note:
    reload(module)
    
    ## This function that reloads a module. This can be extremely useful during development if you need to update a module and reload it without terminating your program. However, objects created before the module is reloaded are not updated, so you must be careful in handling those objects.

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
