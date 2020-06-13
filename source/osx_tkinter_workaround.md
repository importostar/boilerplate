---
title: osx_tkinter_workaround
date: 2020-05-07
---
Example Python program osx_tkinter_workaround.py

## Modules

* from easygui import msgbox
* from Tkinter import Tk
* from subprocess import Popen, PIPE
* from re import search

## Code

Python tkinter example

    #!/usr/bin/env python
    
    ## This script demonstrates a workaround for the Tkinter (Tcl/Tk?) activation
    ## bug under OS X. More on that here:
    ##  http://groups.google.com/group/comp.lang.python/browse_thread/thread/64f3bc64de5dc773/973c208be03d1514
    ##  
    ##  - Nick Fisher
    
    from easygui import msgbox
    from Tkinter import Tk
    from subprocess import Popen, PIPE
    from re import search
    
    ## Force the Tk subsystem to initalize so it can be manipulated
    ## A blunt way around the chicken/egg problem with trying to bring a UI to the 
    ## foreground when it doesn't exsist yet.
    t = Tk()
    # Hope that the destroy is fast enough not to be seen (is for me)
    t.destroy()
    
    ## Find the path for Python.app; A little less fragile than hardcodeing...
    # Find the script's process command
    find_cmd_str = 'ps -o command | grep "%s"'%__file__
    find_results = Popen(find_cmd_str, shell=True, stdout=PIPE).stdout.read()
    # Pull out the interpreter app path
    py_path = search('(.*Python\.app)', find_results).groups()[0]
    
    ## Use 'open' to bring Python.app to the foreground...
    ## If there is more than one instance of the same Python.app with a running UI 
    ## then there is trouble. There is no way (I can find) to tell 'open' which 
    ## Python.app to activate.
    # Use the OSX command 'open' to bring Python.app to the foreground
    Popen(['open',py_path])
    
    ## Start using Tkinter/EasyGUI/Grun with the interface in the Foreground
    msgbox('Hello world!')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
