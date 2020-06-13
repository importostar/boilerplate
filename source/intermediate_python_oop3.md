---
title: intermediate_python_oop3
date: 2020-05-07
---
Example Python program intermediate_python_oop3.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class company:

## Methods

* def __init__(self,Profile):
* def office_hours(self,start_time,finish_time):

## Code

Python example

    class company:
        
        ## Class variable
        welcome_msg = 'Welcome to Robofied!'
        
        ## Constructor function called while creating object.
        def __init__(self,Profile):
            
            self.Profile = Profile
            print('Welcome to {} team!'.format(self.Profile))
    
        ## User defined function for calculting hours
        def office_hours(self,start_time,finish_time):
            
            ## How to access class variable inside function
            
            print(self.welcome_msg)
            
            ## We can access variable passed to constructor function here as well.
            
            """This is because that variable is associated with object and self is basically for your understanding 
            we can say it represents object"""
            
            print('Welcome to {} team!'.format(self.Profile))
            
            ## variables inside the function only
            ## instance variable
            self.start_time = start_time
            self.finish_time = finish_time
            
            print('Your office hours will be ' + str((int(self.finish_time.split(':')[0]) - int(self.start_time.split(':')[0])))+ 
                  ' hours.')
            
    full_stack = company('Full stack developer')
    
    #[Output]:
    #Welcome to Full stack developer team!
    
    full_stack.office_hours('9:00','18:00')
    
    #[Output]:
    #Welcome to Robofied!
    #Welcome to Full stack developer team!
    #Your office hours will be 9 hours.
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
