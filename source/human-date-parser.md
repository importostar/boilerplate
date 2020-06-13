---
title: human date parser
date: 2020-05-07
---
Example Python program human-date-parser.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function # Need to grab the print function from Python 3.
* import parsedatetime # Requires "parsedatetime" Python module
* from datetime import datetime
* import argparse
* 		from Tkinter import Tk # Might need to get tkinter from your package manager on Linux.
* 		from tkinter import Tk # Fix for Python 3, which changed the case of Tkinter.

## Code

Python tkinter example

    #!/usr/bin/python
    
    from __future__ import print_function # Need to grab the print function from Python 3.
    
    import parsedatetime # Requires "parsedatetime" Python module
    
    from datetime import datetime
    import argparse
    
    argparser = argparse.ArgumentParser()
    
    argparser.add_argument("input", nargs='?', help="text to convert into a date.")
    argparser.add_argument("-d", "--dash", action="store_true", help="use dashes instead of slashes as a seperator.")
    argparser.add_argument("-g", "--github", action="store_true", help="output in GitHub dashed format, i.e. \"yyyy-mm-dd\"")
    
    args = argparser.parse_args()
    
    if args.dash or args.github:
    	dateSeparator = "-"
    else:
    	dateSeparator = "/"
    
    if not args.input: # If there's nothing on the command line, read from the clipboard.
    	try:
    		from Tkinter import Tk # Might need to get tkinter from your package manager on Linux.
    	except:
    		from tkinter import Tk # Fix for Python 3, which changed the case of Tkinter.
    	r = Tk()
    	r.withdraw()
    
    	result = r.selection_get(selection = "CLIPBOARD")
    else:
    	result = args.input
    
    cal = parsedatetime.Calendar()
    
    time_struct, parse_status = cal.parse(result)
    parsedDate = datetime(*time_struct[:6])
    if not args.github:
    	printDate = str(parsedDate.month) + dateSeparator + str(parsedDate.day) + dateSeparator + str(parsedDate.year) # Using the admittedly horrible American date format.
    else:
    	printDate = str(parsedDate.year) + dateSeparator + str(parsedDate.month).zfill(2) + dateSeparator + str(parsedDate.day).zfill(2)
    
    print(printDate, end="")
    
    # r.clipboard_clear()
    # r.clipboard_append(printDate) # Code to send to clipboard, broken in Python 3, worked around by printing output and piping to clip.exe/xsel -ib
    if not args.input:
    	r.destroy()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
