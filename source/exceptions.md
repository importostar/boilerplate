---
title: exceptions
date: 2020-05-07
---
Example Python program exceptions.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import sys
* import sys
* import sys

## Classes

* class CustomValueError(ValueError):

## Methods

* def __init__(self, arg):

## Code

Python example

    #Generic exception handling
    try:
        Value = int(input("Type a number between 1 and 10: "))
    except:
        print("You must type a number between 1 and 10!")
    else:
        if (Value > 0) and (Value <= 10):
            print("You typed: ", Value)
        else:
            print("The value you typed is incorrect!")
          
    '''
    Type a number between 1 and 10: a
    You must type a number between 1 and 10!
    
    Type a number between 1 and 10: a
    You must type a number between 1 and 10!
    -----------------------------------------------------------------
    '''
    
    #Basic exception handling
    try:
        Value = int(input("Type a number between 1 and 10: "))
    except ValueError:
        print("You must type a number between 1 and 10!")
    else:
        if (Value > 0) and (Value <= 10):
            print("You typed: ", Value)
        else:
            print("The value you typed is incorrect!")
            
    '''
    Type a number between 1 and 10: 1
    You typed:  1
    
    Type a number between 1 and 10: a
    You must type a number between 1 and 10!
    -----------------------------------------------------------------
    '''
    
    #Multiple exceptions with single except clause
    try:
        Value = int(input("Type a number between 1 and 10: "))
    except (ValueError, KeyboardInterrupt):
        print("You must type a number between 1 and 10!")
    else:
        if (Value > 0) and (Value <= 10):
            print("You typed: ", Value)
        else:
            print("The value you typed is incorrect!")
            
    '''
    Type a number between 1 and 10: 1
    You typed:  1
    
    Type a number between 1 and 10: a
    You must type a number between 1 and 10!
    -----------------------------------------------------------------
    '''
    
    #Multiple exceptions with multiple except clauses no.1
    try:
        Value = int(input("Type a number between 1 and 10:"))
    except ValueError:
        print("You must type a number between 1 and 10!")
    except KeyboardInterrupt:
        print("You pressed Ctrl+C!")
    else:
        if (Value > 0) and (Value <= 10):
            print("You typed: ", Value)
        else:
            print("The value you typed is incorrect!")
            
    '''
    Type a number between 1 and 10:1
    You typed:  1
    >>> 
    Type a number between 1 and 10:a
    You must type a number between 1 and 10!
    >>> 
    Type a number between 1 and 10:
    You pressed Ctrl+C! => (when you press Cancel button)
    -----------------------------------------------------------------
    '''
    
    #Exception with argument
    import sys
    try:
        File = open('myfile.txt')
    except IOError as e:
        print("Error opening file!\r\n" +
         "Error Number: {0}\r\n".format(e.errno) +
         "Error Text: {0}".format(e.strerror))
    else:
        print("File opened as expected.")
        File.close();
        
    '''
    Error opening file!
    Error Number: 2
    Error Text: No such file or directory
    -----------------------------------------------------------------
    '''
    
    #List of arguments
    import sys
    try:
        File = open('myfile.txt')
    except IOError as e:
        for Arg in e.args:
            print(Arg)
    else:
        print("File opened as expected.")
        File.close();
        
    '''
    2
    No such file or directory
    -----------------------------------------------------------------
    '''
    
    #List of arguments with names
    import sys
    try:
        File = open('myfile.txt')
    except IOError as e:
        for Entry in dir(e):
            if (not Entry.startswith("_")):
                try:
                    print(Entry, " = ", e.__getattribute__(Entry))
                except AttributeError:
                    print("Attribute ", Entry, " not accessible.")
    else:
        print("File opened as expected.")
        File.close();
        
    '''
    args  =  (2, 'No such file or directory')
    Attribute  characters_written  not accessible.
    errno  =  2
    filename  =  myfile.txt
    filename2  =  None
    strerror  =  No such file or directory
    winerror  =  None
    with_traceback  =  <built-in method with_traceback of FileNotFoundError object at 0x00000000045FABC0>
    -----------------------------------------------------------------
    '''
    
    #Multiple exceptions with multiple except clauses no.2
    try:
        Value1 = int(input("Type the first number: "))
        Value2 = int(input("Type the second number: "))
        Output = Value1 / Value2
    except ValueError:
        print("You must type a whole number!")
    except KeyboardInterrupt:
        print("You pressed Ctrl+C!")
    except ZeroDivisionError:
        print("Attempted to divide by zero!")
    except ArithmeticError:
        print("An undefined math error occurred.")
    else:
        print(Output) #if no errors then print Value1/Value2
    
    '''
    Type the first number: 1
    Type the second number: 1
    1.0
    
    Type the first number: 
    You pressed Ctrl+C!
    
    Type the first number: 1
    Type the second number: 0
    Attempted to divide by zero!
    -----------------------------------------------------------------
    '''
    
    #Nested exceptions with 'try again' input
    TryAgain = True
    while TryAgain: #Loop until you entered integer number
        try:
            Value = int(input("Type a whole number. "))
        except ValueError:
            print("You must type a whole number!")
            try:
                DoOver = input("Try again (y/n)? ")  #Try again y=Yes, n=No
            except:
                print("OK, see you next time!")
                TryAgain = False
            else:
                if (str.upper(DoOver) == "N"):
                    TryAgain = False
        except KeyboardInterrupt:
            print("You pressed Ctrl+C!")
            print("See you next time!")
            TryAgain = False
        else:
            print(Value)
            TryAgain = False
    '''
    -----------------------------------------------------------------
    '''
    
    #Raise exception
    try:
        raise ValueError
    except ValueError:
        print ("ValueError Exception Raised!")
    
    '''
    ValueError Exception Raised!
    -----------------------------------------------------------------
    '''
    
    #Raise excweption with passing user error information
    try:
        Ex = ValueError()
        Ex.userMessage = "Value Error"
        raise ValueError
    except ValueError:
        print(Ex.userMessage)
        
    '''
    Value Error
    -----------------------------------------------------------------
    '''
    
    #Custom raise exception
    class CustomValueError(ValueError):
        def __init__(self, arg):
            self.strerror = arg
            self.args = {arg}
    
    
    try:
        raise CustomValueError("Value must be within 1 and 10.")
    except CustomValueError as e:
        print("CustomValueError Exception!", e.strerror)
    
    '''
    CustomValueError Exception! Value must be within 1 and 10.
    -----------------------------------------------------------------
    '''
    
    #Raise exception with finally clause
    import sys
    try:
        raise ValueError
        print("Raising an exception.")
    except ValueError:
        print("ValueError Exception!")
        sys.exit()
    finally:
        print("Taking care of last minute details.")
        
    '''
    ValueError Exception!
    Taking care of last minute details.
    '''

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
