---
title: Snipplr 51486
date: 2020-05-07
---
Example Python program Snipplr-51486.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* import shutil
* import shutil
* import os,shutil 

## Methods

* def renamer(target) :

## Code

Python example

    # simply
    import os
    os.rename('a.txt','b.kml')
    
    # or
    
    import shutil
    shutil.move('a.txt', 'b.kml')
    
    
    # or if you want to copy..
    
    import shutil
    shutil.copy('a.txt', 'b.kml')
    
    
    
    
    
    # 
    # Another example: I am trying to rename a list of files:
    # 
    # File1.File1
    # File2.File2
    # 
    # etc
    # 
    # I need them to be renamed to:
    # 
    # File1
    # File2
    # etc
    
    
    
    
    import os,shutil 
       
    def renamer(target) :    
        os.chdir(target)
        for filename in os.listdir('.') :
            print filename
            newfilename = os.path.splitext(filename)[0] 
            print newfilename
            os.rename(filename, newfilename)
            print "Renamed " + filename + " to " + new_filename
    
    # test the function/module
    if __name__ == __main__:
        renamer(sys.argv[1])
    
    
    # or more simply:

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
