---
title: os
date: 2020-05-07
---
Example Python program os.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import os 

## Code

Python example

    import os
    
    # Returns current directory
    os.getcwd()
    
    # Returns absolute path on your system 
    os.path.abspath('.')  
      
    # Returns files and directories in the current directory on your system 
    os.listdir('.')
    
    # isdir function 
    # This function specifies whether the path is existing directory or not. 
    import os 
    out = os.path.isdir("C:\\Users") 
    print(out) 
    
    #####################################################
    
    # Path 
    path = "/home"  
    # Join various path components  
    print(os.path.join(path, "User/Desktop", "file.txt")) 
    
    /home/User/Desktop/file.txt
    
    # Path 
    path = "/home"
    # Join various path components  
    print(os.path.join(path, "User/Public/", "Documents", "")) 
      
    # In above example the last path component is empty so a directory seperator ('/') will be put at the end along with the concatenated value 
    
    /home/User/Public/Documents/
    
    #####################################################
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
