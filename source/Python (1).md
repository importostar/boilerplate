---
title: Python (1)
date: 2020-05-07
---
Example Python program Python (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random
* import os 
* import sys

## Classes

* class Pet: 

## Methods

* def Numberadd(fNum, sNum):
* def __init__(self, name, height, weight, sound):
* def set_name(self, name):
* def set_height(self, height):
* def set__weight(self, weight):
* def set_sound(self, sound):
* def get_name(self):
* def get_height(self):
* def get_weight(self):
* def get_sound(self):
* def get_stype(self):
* def toString(self):

## Code

Python example

    #Import. We use this to make functions available
    # These are called modules
    import random
    import os 
    import sys
    ''' Multi Line Comment '''
    # Single Line Comment
    ''' Hello World '''
    print("Hello World")
    ''' Setting a variable'''
    name = "Naseem"
    print(name)
    # Variables can store 5 data types. Strings, Lists(Arrays), Tuple, Dictionary.
    # You can store any of them in the same Variables
    age = 15
    print(name, "is", age)
    # Arithmetic operators are +, -, *, /, %, **, //
    # ** Exponential Calculation
    # // Floor Division
    print("5 + 2 =", 5+2)
    print("5 - 2 =", 5-2)
    print("5 * 2 =", 5*2)
    print("5 / 2 =", 5/2)
    print("5 % 2 =", 5%2)
    print("5 ** 2 =", 5**2)
    print("5 // 2 =", 5//2)
    
    # Order of Operatings applies to Python
    print('1 + 2 - 3 * 2 =', 1 + 2 - 3 * 2) # = -3
    print("(1 + 2 - 3) * 2 =", (1 + 2 - 3) * 3) # = 0
    
    # String is a string of characters with "" or my favorite ''
    
    not_float = "This isn\'t a float"
    # Use \ if you need to use '' or "" between the same qoute.
    ''' Multi Line Qoute Below '''
    multi_line = ''' Just like
    a Multi Line Comment '''
    # If you hate newlines and don't want them use end=""
    # Not \n. You know who you are
    print('I hate ',end="")
    print('newlines')
    # You are able to print strings multiple times
    print('newlines' * 9)
    # Arrays aka Lists
    
    example_list = [ 'List1', 'List2', 'List3', 'List4']
    # Lists are indexed at 0. So to print the first item, call the list at 0
    print('The first list is', example_list[0])
    # If you want, you can change the values stored in a list 
    example_list[0] = 'List'
    print(example_list) # New List
    # You can get the subset of the lists with [min:=>max]
    print(example_list[0:4])# Prints List, List2, List3, List4
    # Why not store lists within lists?
    example_list2 = ['List5', 'List6', 'List7', 'List8']
    total_lists = [example_list, example_list2] # Listception
    print(total_lists)
    # Listception part 2 
    ''' Getting the second item from both list '''
    print(total_lists[1][1])
    ''' Adding Values using append ''' 
    example_list2.append('List9')
    print(example_list2)
    # Inserting an item at a specifc index
    example_list2.insert(11, "List10")
    print(example_list2)
    # Changed my mind
    example_list2.remove("List10")
    #Time to sort
    example_list2.sort()
    # Nevermind
    example_list2.reverse()
    # Unadoption?
    del example_list2[0]
    # How big?
    print(len(total_lists))
    #Max?
    print(max(total_lists))
    #Min?
    print(min(total_lists))
    #Donkey?
    total_lists.append("Donkey")
    #Tuples Time.
    ''' Tuples are lists that have data that cannot be edited.
    Think of them as ledgers. Data stored in a tuple is permanent
    '''
    example_tuple = (1, 2 ,3, 4, 5)
    #Change list to tuple
    tuple_total_list = tuple(total_lists)
    
    # Are you lost? 'Cause it's map Time
    
    example_map = {'Map1' : 'Map2', 'Map3' : 'Map4', 'Map5' : 'Map6'}
    print(example_map['Map1'])
    # When setting a map, ":"  equals "="
    # You can perform the same tasks as lists. Such as del, and len 
    #Get values for passed keys
    print(example_map.get("Map2"))
    # Get a list of keys
    print(example_map.keys())
    # Get a list of map values
    print(example_map.values())
    
    # If, Elif, Else 
    developers = 2
    if developers > 2 : 
        print("We have 2 Developers")
    elif developers >= 2 :
        print("We have 2 Developers")
    else:
        print("Wrong amount of Developers")
    # With If, Elif, and Else statments. You can include, and, or, not.
    # Loop Time
    #Allow you to perform an action a set number of times
    #Range performs the action 5 times 0-4
    for x in range(0, 5):
        print(x , ' ', end="")
        
    print('\n')
    
    # Cycle through lists
    for y in example_list2:
        print(y)
        
    # Double up loops to cycle through lists
    num_list =[[1,2,3],[10,20,30],[100,200,300]];
     
    for x in range(0,3):
        for y in range(0,3):
            print(num_list[x][y])
    
    #While?
    random_num = random.randrange(0,150)
    while (random_num != 6):
        print(random_num)
        random_num = random.randrange(0,100)
    #Iterator?
    i = 0;
    while (1 <= 20):
        if(i%2 ==0):
            print(i)
        elif(i == 9):
            break #Ends loop
        else:
            #Shorthand for i = i + i
            i += 1
            #Skips
            continue
        i += 1
        
    #Time to get with the Function 
    #Functions let use reusde code 
    def Numberadd(fNum, sNum):
        sumNum = fNum + sNum
        return sumNum
    print(Numberadd(6, 6))
    
    # Thanks to scope. we cannot get the value of rNumbecause it is in the Functions
    
    
    # User Input Time
    print("What\'s your favorite color?")
    fave_color = sys.stdin.readline()
    print("Your favorite color is", fave_color)
    
    
    # strings
    
    example_string = "This is a string"
    # Get the first 5 characters
    print(example_string[0:50])
    # Get the last 5 characters
    print(example_string[-5:])
    # Get everything up to the last 5 characters
    print(example_string[:-5])
    #Formatting
    #Capitalizes the First letter
    print(example_string.capitalize())
    #Return index
    print(example_string.find("This"))
    #This is case sensitive ^^^^^^^^^^
    
    #Returns true if all characters are numbers
    # " and ' are characters
    print(example_string.isalpha())
    print(example_string.isalnum())
    ## FILE I/O. INPUT/OUTPUT
    
    example_file = open("example.txt", "wb")
    
    print(example_file.mode) # Gets file mode 
    print(example_file.name)
    
    example_file.write(bytes("Write me to a file\n", 'UTF-8'))
    
    example_file.close() # Closes file 
    example_file = open("example_text.txt", "r+") # Opens file for reading/writing
    
    example_text = example_file.read() # Read file example_text
    
    print(example_text)
    
    os.remove("example_text.txt") # Delete file 
    
    
    #Classes and objects
    #Classes allow you to model real world things using code
    class Pet: 
        
        #You can hide a variable by making it private with __
        
        __name = None
        __height = None
        __weight = None
        __sound = None
        
        def __init__(self, name, height, weight, sound):
            
            self.__name = name
            self.__height = height
            self.__weight = weight
            self.__sound = sound 
        def set_name(self, name):
            self.__name = name 
        def set_height(self, height):
            self.__height = height
        def set__weight(self, weight):
            self.__weight = weight
        def set_sound(self, sound):
            self.__sound = sound
        def get_name(self):
            return self.__name
        def get_height(self):
            return str(self.__height)
        def get_weight(self):
            return str(self.__weight)
        def get_sound(self):
            return self.__sound
        def get_stype(self):
            print("Pet")
        def toString(self):
            return "{} is {} cm tall and {} kilograms and says {}".format(self.__name, self.__height, self.__weight, self.__sound)
            
    # Hot to create a Pet object 
    dog = Pet('Spots', 32, 10, 'Woof')
    print(dog.toString())
    
    # DONE

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
