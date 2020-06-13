---
title: racional
date: 2020-05-07
---
Example Python program racional.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import math

## Classes

* class Racional:

## Methods

* 	def __init__(self, dividendo, divisor):
* 	def __str__(self):
* 	def __mul__(self, outro):
* 	def __add__(self, outro):
* 	def highestCommonFactor(a, b):
* 	def leastCommonMultiple(a,b): 

## Code

Python example

    import math
    
    class Racional:
    	def __init__(self, dividendo, divisor):
    		self.divisor = divisor
    		self.dividendo = dividendo
    	
    	def __str__(self):
    		return str(self.dividendo) + '/' + str(self.divisor)
    
    	def __mul__(self, outro):
    		divisor = self.divisor * outro.divisor
    		dividendo = self.dividendo * outro.dividendo
    		return new Racional(dividendo, divisor)
    
    	def __add__(self, outro):
    		commonMultiple = Racional.leastCommonMultiple(self.divisor. outro.divisor)
    
    		dividendo1 = self.dividendo * (commonMultiple/self.divisor)
    		dividendo2 = outro.dividendo * (commonMultiple/outro.divisor)
    
    		return new Racional(dividendo1+dividendo2, commonMultiple)
    
    	def highestCommonFactor(a, b):
    		return a if b == 0 else Racional.highestCommonFactor(b, (a%b))
    
    	def leastCommonMultiple(a,b): 
    	    return a * b / Racional.highestCommonFactor(a,b)
    	
    
    
    a = Racional(1,2)
    b = Racional(3,4) 
    
    c = a*b
    d = a+b
    print("Seja o racional a = ",a)
    print("Seja o racional b = ",b)
    print("Seja o racional c (a * b) = ",c)
    print("Seja o racional c (a + b) = ",d)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
