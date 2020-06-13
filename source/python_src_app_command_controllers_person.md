---
title: python_src_app_command_controllers_person
date: 2020-05-07
---
Example Python program python_src_app_command_controllers_person.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from base import BaseController

## Classes

* class PersonController (BaseController):

## Methods

* def __init__ (self):
* def dashboard (self):
* def list (self):
* def info (self, id = None):

## Code

Python example

    from base import BaseController
    
    class PersonController (BaseController):
    
    
        def __init__ (self):
            self.dashboard()
    
    
        def dashboard (self):
            print 'Person Dashboard'
            self.input(
                operations = {
                    '0': { 'name': 'Back', 'do': 'back' },
                    '1': { 'name': 'List', 'do': 'list' },
                    '2': { 'name': 'Info', 'do': 'info' }
                }
            )
    
    
        def list (self):
            print 'Person List'
            self.input(
                operations = {
                    '0': { 'name': 'Back', 'do': 'back' }
                }
            )
    
    
        def info (self, id = None):
            if not id:
                id = raw_input('Please input the info id: ')
    
            self.input(
                operations = {
                    '0': { 'name': 'Back', 'do': 'back' }
                }
            )
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
