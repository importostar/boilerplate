---
title: logging_example
date: 2020-05-07
---
Example Python program logging_example.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import logging

## Methods

* def factorial(n):

## Code

Python example

    # add logging.disable(logging.CRITICAL) for disable logging
    import logging
    
    logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s - %(levelname)s
    - %(message)s')
    logging.debug('Start of program')
    
    def factorial(n):
      logging.debug('Start of factorial( %)' % (n))
      total = 1
      for i in range(n + 1):
        total *= i
        logging.debug('i is ' + str(i) + ', total is ' + str(total))
        logging.debug('End of factorial( %)' % (n))
      return total
    
    print(factorial(5))
    logging.debug('End of program')
                        
    # Logging to a text file:
    logging.basicConfig(filename='myProgramLog.txt', level=logging.DEBUG, format='
    %(asctime)s - %(levelname)s - %(message)s')                    
                        
                        
    """
    Logging levels
    Logging Function
    Description
    DEBUG
    logging.debug()
    The lowest level. Used for small details. 
    Usually you care about these messages only when diagnosing problems.
    INFO
    logging.info()
    Used to record information on general events in your program or confirm that things are working at their point in the program.
    WARNING
    logging.warning()
    Used to indicate a potential problem that doesn’t prevent the program from working but might do so in the future.
    ERROR
    logging.error()
    Used to record an error that caused the program to fail to do something.
    CRITICAL
    logging.critical()
    The highest level. 
    Used to indicate a fatal error that has caused or is about to cause the program to stop running entirely."""

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
