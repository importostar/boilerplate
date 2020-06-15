---
title: Snipplr 25249
date: 2020-05-07
---
Example Python program Snipplr-25249.py


## Code

Python example

    # The os module provides a portable platform-independent interface to access common operating services,
    # allowing you to add OS-level support to your programs.
    
    # The os.path.abspath(path) function of the os module returns a string version of the absolute path of the
    # path specified. Because abspath takes into account the current working directory, the . and .. directory
    # options will work as shown next:
    
    >>>print os.path.abspath(".") 
    >>>C:\books\python\ch1\ print os.path.abspath("..") C:\books\python\
    
    ## The os.path module provides the exists(path), isdir(path), and isfile(path) function to check for the
    # existence of files and directories, as shown here:
    
    >>>print os.path.exists("/books/python/ch1") 
    True 
    >>>print os.path.isdir("/books/python/ch1") 
    True 
    >>>print
    os.path.isfile("/books/python/ch1/ch1.doc") 
    True
    
    ## The os.chdir(path) function provides a simple way of changing the current working directory for the program,
    # as follows:
    
    >>>os.chdir("/books/python/ch1/code") 
    >>>print os.path.abspath(".") 
    C:\books\python\CH1\code
    
    ## The os.environ attribute contains a dictionary of environmental variables. You can use this dictionary as
    # shown next to access the environmental variables of the system:
    
    >>>print os.environ['PATH'] 
    C:\WINNT\system32;C:\WINNT;C:\Python24
    
    ## The os.system(command) function will execute a system function as if it were in a subshell, as shown with
    # the following dir command:
    
    >>>os.system("dir") 
    Volume Serial Number is 98F3-A875
     Directory of C:\books\python\ch1\code
    08/11/2006  02:10p      <DIR>          .
    08/11/2006  02:10p      <DIR>          ..
    08/10/2006  04:00p                 405 format.py
    08/10/2006  10:27a                 546 function.py
    08/10/2006  03:07p                 737 scope.py
    08/11/2006  02:58p                 791 sys_tools.py
                   4 File(s)          3,717 bytes
                   2 Dir(s)   7,880,230,400 bytes free
    
    ## Python provides a number of exec type functions to execute applications on the native system. The following
    # example illustrates using the os.execvp(path, args) function to execute the application update.exe with a
    # command-line parameter of -verbose:
    
    >>>os.execvp("update.exe", ["-verbose"])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
