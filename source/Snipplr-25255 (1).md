---
title: Snipplr 25255 (1)
date: 2020-05-07
---
Example Python program Snipplr-25255 (1).py

## Modules

* ## Modules can be imported directly using the package or module name. Items in submodules must be accessed explicitly including the full package name.
* &gt;&gt;&gt; import os
* ## Modules can be imported directly using the module name, but the namespace should be named something different. Items in submodules must be accessed explicitly including the full package name:
* &gt;&gt;&gt; import os as computer
* ## Modules can be imported using the module name within the package name. Items in submodules must be accessed explicitly including the full package name:
* &gt;&gt;&gt; import os.path
* ## Modules can be imported by importing the modules specifically from the package. Items in submodules can be accessed implicitly without the package name:
* &gt;&gt;&gt; from os import path

## Code

Python example

    ## Modules can be imported directly using the package or module name. Items in submodules must be accessed explicitly including the full package name.
    
    &gt;&gt;&gt; import os
    &gt;&gt;&gt; os.path.abspath(&quot;.&quot;)
    'C:\\books\\python'
    
    
    ## Modules can be imported directly using the module name, but the namespace should be named something different. Items in submodules must be accessed explicitly including the full package name:
    
    &gt;&gt;&gt; import os as computer
    &gt;&gt;&gt; computer.path.abspath(&quot;.&quot;)
    'C:\\books\\python'
    
    
    ## Modules can be imported using the module name within the package name. Items in submodules must be accessed explicitly including the full package name:
    
    &gt;&gt;&gt; import os.path
    &gt;&gt;&gt; os.path.abspath(&quot;.&quot;)
    'C:\\books\\python'
    
    
    ## Modules can be imported by importing the modules specifically from the package. Items in submodules can be accessed implicitly without the package name:
    
    &gt;&gt;&gt; from os import path
    &gt;&gt;&gt; path.abspath(&quot;.&quot;)
    'C:\\books\\python'
    
    
    ## Note:
    reload(module)
    
    ## This function that reloads a module. This can be extremely useful during development if you need to update a module and reload it without terminating your program. However, objects created before the module is reloaded are not updated, so you must be careful in handling those objects.

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
