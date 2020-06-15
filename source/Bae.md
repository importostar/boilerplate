---
title: Bae
date: 2020-05-07
---
Example Python program Bae.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class Bae:
* # the class variable can also be accesed by instances : we write self.much

## Methods

* def __init__(self, first, last, grade, classement):
* def raisement(self):
* def setup(cls, amount):

## Code

Python example

    class Bae:
        """dtring for Bae"""
        much = 1.50  # class variable
        students = 0  # we use is class variable to count the number of instances in this classes
    
        def __init__(self, first, last, grade, classement):
            self.first = first  # These are atributes for the class
            self.last = last
            self.grade = grade
            self.classement = classement
    
            Bae.students += 1  # counter for instances
    
        def raisement(self):
            self.grade = int(
                self.grade * Bae.much)  # how much are we going to add in grade / this is a methode called raisement
    
        # the class variable can also be accesed by instances : we write self.much
    
        @classmethod
        def setup(cls, amount):
            cls.much = amount
    
    
    std_1 = Bae('Aymen', 'Akrouf', 14, 4)  # this is an instance of a class
    std_2 = Bae('Aziz', 'Zermout', 20, 1)
    
    Bae.setup(1.08)
    
    print(Bae.much)
    print(std_1.much)
    print(std_2.much)
    
    print(Bae.students)  # counter
    print(std_1.grade)
    
    std_1.raisement()  # this is where we introduced the methode within the instance
    print(std_1.grade)
    
    print(std_2.first + ' ' + std_2.last, std_2.grade)
    print('{} {}'.format(std_1.first, std_1.last))
    
    print(std_1.much)  # here we can see that we are accessing the class variable using the instance
    
    print(std_1.__dict__)
    std_1.much = 1.40
    std_1.raisement()  # here we are introducing the methode again
    print(std_1.__dict__)
    print(std_1.much)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
