---
title: Snipplr 25247
date: 2020-05-07
---
Example Python program Snipplr-25247.py


## Code

Python example

    ## The platform module provides a portable interface to information about the platform on which the program is being executed. ## The following examples illustrate some of the most common uses of the platform module.
    
    ## The platform.architecture() function returns the (bits, linkage) tuple that specifies the number of bits for the system word size and linkage information about the Python executable:
    
    >>>print platform.architecture()
    ('32bit', '')
    
    ##The platform.python_version() function returns the version of the Python executable for compatibility purposes:
    
    >>>print platform.python_version()
    2.4.2
    
    ## The platform.uname() function returns a tuple in the form of (system, node, release, version, machine, processor). System refers to which OS is currently running, node refers to the host name of the machine, release refers to the major release of the OS, version refers to a string representing OS release information, and machine and processor refer to the hardware platform information.
    
    >>>print platform.uname()
    ('Linux', 'bwd-linux', '2.6.16-20-smp',
     '#1 SMP Mon Apr 10 04:51:13 UTC 2006',
     'i686', 'i686')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
