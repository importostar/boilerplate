---
title: undersocre
date: 2020-05-07
---
Example Python program undersocre.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* # note that is is ignored in import calls but still reachable with direct calls

## Classes

* class A:

## Methods

* def _internal_function(self): 
* 	def __init__(self, val):
* def __double_method(self):

## Code

Python example

    #python 3
    
    # throw out some values
    
    a, b, _ = (1, 2, 3)
    
    a, *_ = (1, 2, 3, 4, 5) # a=1
    
    a, _, b, *_ = (1, 2, 3, 4, 5) # a=1, b=3
    
    # for iterator
    
    for _ in range(10): # execute fn for ten times
    	fn()
      
    for _, val in enumerate(dictdict): # it print keys
    	print(val)
        
    # _single_leading_underscores
    
    # note that is is ignored in import calls but still reachable with direct calls
    
    _internal_variable = 'thinkthink'
    
    def _internal_function(self): 
    	return _internal_varialbe
    
    # __double_leading_underscores
    
    # it is more like a syntactic sugar
    # in this case method, mangling happens as _A_double_method 
    
    class A:
    	def __init__(self, val):
        	self.val = val
    
        def __double_method(self):
        	pass
    
    
    # used as i18n / l10n function
    
    translated: string = _("sometextthatneedtranslate")
    
    # for number literal
    
    dec = 1_000_000
    bin = 0b_1111_0000
    hex = 0x_1234_abcd

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
