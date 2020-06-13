---
title: cheat_5
date: 2020-05-07
---
Example Python program cheat_5.py
For Python version 2.x.
To test your Python version use:

    python --version


## Classes

* class Bank():

## Methods

* def even_numbers_generator(start):
* def next_number_generator(step):
* def create_atm(self):

## Code

Python example

    """
    CHEAT 5: yield
    
    Generators are iterators, but you can only iterate over them once. It's because they do not
    store all the values in memory, they generate the values on the fly.
    Yield is a keyword that is used like return, except the function will return a generator.
    
    http://freepythontips.wordpress.com/2013/09/29/the-python-yield-keyword-explained/
    http://www.alvarohurtado.es/generadores-en-python/
    """
    
    #example 1
    def even_numbers_generator(start):
        a = start
        while a < 20:
            a += 2
            yield a
    #test
    for number in even_numbers_generator(8):
        print number
    number = even_numbers_generator(8)
    print number.next() # invoke next() method explicity
    print number.next()
    
    #result
    """
    10
    12
    14
    16
    18
    20
    10
    12
    """
    
    #example 2
    def next_number_generator(step):
        try:
            a = 0
            while True:
                yield a
                a += step
        finally:
            print "finish!"
            
    #test
    generator = next_number_generator(3)
    print generator.send(None) # you're using send to "start" a generator (that is, execute the code from the
                               # first line of the generator function up to the first yield statement)
    print generator.next()
    print generator.next()
    generator.close() # close method generates exception into next_number_generator method
    print generator.next() # error
    
    #result
    """
    10
    12
    14
    16
    18
    20
    10
    12
    0
    3
    6
    finish!
    
    Traceback (most recent call last):
    ...
    StopIteration
    """
    
    #example 3
    class Bank():
        crisis = False
        def create_atm(self):
            while not self.crisis:
                yield "$100"
                
    #test
    bank = Bank() 
    corner_street_atm = bank.create_atm()
    print(corner_street_atm.next())
    print(corner_street_atm.next())
    print([corner_street_atm.next() for cash in range(5)])
    bank.crisis = True # no more money
    print(corner_street_atm.next()) # error
    
    #result
    """
    $100
    $100
    ['$100', '$100', '$100', '$100', '$100']
    
    Traceback (most recent call last):
    ...
    StopIteration
    """

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
