---
title: python_basic
date: 2020-05-07
---
Example Python program python_basic.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* #import decimal

## Code

Python example

    %reset -f
    #%%
    #Numbers
    print(2+2)
    print(2*2)
    print(5-3)
    print(4/2)
    #the calculation will happen as per per arithmatic precedence
    print(2*2+3-4)
    print(9*5+1-7)
    print(3*2+2-3)
    print(4*6+9-1)
    print(4*9+7+1)
    print(4*9+3-1)
    #this is happening as() has more arithmatic precedence then * 
    print(2*(2+3))
    #different data type used in python(int,float,string,byte,list)
    type(6)
    type(6.4)
    type(7.5)
    type(3.2)
    type(2.8)
    type(9.9)
    type('3.7')
    type('6.4')
    type('4.2')
    type('1.9')
    type('8.3')
    type('1.4')
    #Python supports a range of types to store sequences. There are six sequence 
    #types: strings, byte sequences (bytes objects), byte arrays (bytearray objects),
    # lists, tuples, and range objects.
    #sequence:Sequences allow you to store multiple values in an organized and 
    #efficient fashion. There are seven sequence types: strings, Unicode strings, 
    #lists, tuples, bytearrays, buffers, and xrange objects. Dictionaries and sets
    # are containers for sequential data.
    type(b'6.4')
    type([6.4])
    type([2.6])
    type([5.4])
    #works perfectly for bot single and double quotes.
    type(["list"])
    type(["Python"])
    type(["Oracle"])
    type(["Mongo"])
    type(['list'])
    type(['Python'])
    type(['Oracle'])
    type(['Mongo'])
    
    #We can perform a floor division by using two forward slashes (//) 
    #to divide and have the result as an integer.
    4 // 2
    8 // 2
    85 // 5
    75 // 5
    15 // 3
    16 //16
    #modulus operatior will let remain the reminder
    5 % 4
    4 % 2
    96 % 16
    13 % 2
    11 % 5
    12 % 8
    #power using the using two asterisk symbols
    2 ** 4
    3 ** 5
    1 ** 9
    5 ** 4
    # this is the (1/square root) function used against the number
    64 ** (-1/2)
    25 ** (-1/2)
    27 ** (-1/3)
    8878 ** (-1/4)
    1000000 ** (-1/4)
    #exponentiation (**) has higher precedence than * or / or unary -
    4 * - 3 ** 2
    3 * - 3 ** 4
    9 * - 3 ** 2
    4 * - 5 ** 4
    2 * - 7 ** 3 
    #priority is with () i.e.(4 * (-3))
    (5 * (- 5)) ** 2
    (2 * (- 3)) ** 3
    (3 * (- 4)) ** 2
    (4 * (- 1)) ** 4
    (4 * (- 3)) ** 3
    (9 * (- 8)) ** 3
    (6 * (- 6)) ** 2
    #priority is with () i.e.((- 3) ** 2)
    4 * ((- 3) ** 2)
    print(1.1 + 2.2)
    #it will give a 'precesion' upto 15 numbers,to overcome this issue
    #import decimal
    #print(decimal.Decimal(01.1 + 2.2))
    #A complex number is represented as a+bi where a and b are real numbers,
    #like 7 or 12, and i is an imaginary number.
    -1+5.5j
    type(-1+5.5j)
    #as described above it will automatically give a CN as (a+bj)
    complex(3,-2)
    complex(2,-1)
    complex(3.5,-2.9)
    #it will give a complex number automatically.
    Z = complex(3.6, 2.7)
    print(Z)
    #we can check boolean with integers
    bool(1)
    bool(0)
    bool(3j)
    #The following will give a false boolean
    bool(0j)
    bool("")
    #%%
    #Variables
    #Must begin with a letter (a - z, A - B) or underscore (_)
    #Other characters can be letters, numbers or _,Case Sensitive
    #Can be any (reasonable) length
    #A String
    Item_name = "Watch" 
    #An Integer
    Item_qty = 10 
    #a floating number
    Item_value = 1000.23 
    #we can also write this way
    float = float(7.43)
    print(float)
    #using double quotes makes it easy to include apostrophes 
    #(whereas these would terminate the string if using single quotes
    mystring = "Don't worry ! just difference between single and double quotes"
    print(mystring)
    one = 1
    two = 2
    #print(three)
    #the error is "name 'three' is not defined
    three = one + two
    print(three)
    #using single quote and double quote
    s = "A Poor Woman's Journey."
    print(s)
    p = "The dog on the road"
    print(p)
    #it can be written in this way
    a = ("The dog on the road")
    a
    #accessing characters from a string
    a = "Python string"
    a[2]
    a = "Python string"
    a[8]
    a = "Roaring lion"
    a[2]
    a = "Leopard"
    #a[9] -/ error at this line as no text at index 9 exists.
    #ERROR -/string index out of range AS character with index 9 doesn't exist
    #if i want to see the t th charater in the string
    a[4+3]
    #a[2.3] will show an error 'string indices must be integers'
    #implies the character in the reverse order
    a[-2]
    a = "PYTHON"
    #a[0] = "X"
    #ERROR -/ str' object does not support item assignment 
    b = "X"+ a[1]
    print(b)
    #String concatenation
    a = "Python" + "String"
    print(a)
    a = "Python"
    b = "String"
    print(a+b)
    a = "Oracle"
    b = "Database"
    #we can also write it in a differnt way
    a+=b
    print(a)
    a = "Python"
    b = "<" + a*3 +">"
    print(b)
    #String length-/ len() is a built-in function which returns no of characters in a string
    a = "Python"
    len(a)
    #we can try little different thing as follows.
    a = "The morning sunshine"
    b = "is awesome"
    a+=b
    len("print(a)")
    len(a)
    s = "Python"
    #s[1:4] is 'yth' chars starting at index 1 and extending up to but not including index 4
    #s[1:] is 'ython' omitting either index defaults to the start or end of the string
    #s[:] is 'Python'  Copy of the whole thing
    #s[1:100] is 'ython' an index that is too big is truncated down to the string length
    #It also supports the negetive index number count
    #s[-1] is 'n' -- last char (1st from the end)
    #s[-4] is 't' -- 4th from the end
    #s[:-3] is 'pyt' -- going up to but not including the last 3 chars
    #s[-3:] is 'hon' -- starting with the 3rd char from the end and extending to the end of the string.
    a = "Python String"
    print (a[0:5])
    print(a[:8])
    #here the concept START-STOP-STEP comes in to picture.will start at
    a = "Python String"
    print(a[0:3:2])
    #here the concept START-STOP-STEP comes in to picture.will start at 3,
    #stops at t and steps 2x
    a = [ 1, 2, 3, 4, 5, 6, 7, 8]
    print(a[2:7:2])
    a= ('The best way to do it')
    print(a[1:3:4])
    #python string formatting
    #the argument passed here is str.format(*args, **kwargs)
    '{} {}'.format('Python','Format')
    #the same is also for integers
    '{} {}'.format(50, 70)
    #it gives the number as '50 70'
    '{} {}'.format(10,20)
    #'10 20'
    '{} {}'.format('News','Nation')
    # 'News Nation'
    '{1} {0}'.format('News','Nation')
    #'Nation News'
    '{}{}'.format('Qlik', 'View')
    #'QlikView'
    '{1}{0}'.format('Qlik', 'View')
    #'ViewQlik'
    '{0}{0}'.format('Qlik', 'View')
    'QlikQlik'
    '{1}{1}'.format('Qlik', 'View')
    #Padding and aligning strings
    #alligning to the Right(>30)
    '{:>30}'.format('Seychelles')
    #'                    Seychelles'
    #alligning to the left(<40)
    '{:<40}'.format('character')                           '
    #Align center
    '{:^40}'.format('Python')
    '                 Python                 '
    '{:^20}'.format('Newspaper')
    #'     Newspaper      '
    '{:^25}'.format('Formatting')
    '       Formatting        '
    #Truncating the string(it will print till 10 where 10 will be included)
    '{:.10}'.format('Python Schedule')
    #'Python Sch'
    '{:.6}'.format('Application Deployment')
    'Applic'
    #This can be done in a different way,giving the index value at the last.
    '{:.{}}'.format('Application Deployment',10)
    #'Applicatio'
    '{:.{}}'.format('Table of content',12)
    #'Table of con'
    #%%
    #List 
    #the list contains all integer values
    my_list1 = [5, 12, 13, 14] 
    print(my_list1)
    my_list2 = [0, 3, 2, 11]
    print(my_list2)
    my_list3 = [9, 11, 2, 28]
    print(my_list3)
    # the list contains all string
    new_list1 = ['red', 'blue', 'black', 'white']
    print(new_list1)
    new_list2 = ['dog', 'cow', 'sheep', 'cock']
    print(new_list2)
    # the list contains a string, an integer and
    new_list3 = ['blue', 50, 44.20] 
    print(new_list3)
    new_list4 = ['red', 25,50.55] 
    print(new_list4)
    new_list5 = ['black', 28, 11.65] 
    print(new_list5)
    new_list6 = ['yellow', 12, 10.32] 
    print(new_list6)
    c_lst1 = ["White", "Yellow"]
    c_lst2 = ["Red", "Blue"]
    c_lst3 = ["Green", "Black"]
    colours_list = c_lst1 + c_lst2 + c_lst3
    print(colours_list)
    # empty list
    list = []
    print(list)
    #<class 'list'>
    number = [1,2,3,4,5,6,7,8,9]
    print(number[0]*4)
    print(number[2]*5)
    print(number[3]**4)
    print(number[2]**3)
    print(number[-5]**5)
     #Insert an item at third position
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list[2] = "white"
    print(colours_list)
    #another method add a number at certain position
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list.insert(3,"White")
    print(colours_list)
    #Remove an item from the list
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list.remove('Blue')
    print(colours_list)
    #Clearing of all items from a list
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list.clear()
    print(colours_list)
    #List Slicing
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    print(colours_list[0:2])
    print(colours_list[1:3])
    print(colours_list[2:-1])
    print(colours_list[-4:-1])
    #Creates copy of original list
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    print(colours_list[:])
    #Remove the item at the given position in the list, and return it
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    print(colours_list.pop(2))
    print(colours_list)
    #Return the index in the list of the  item
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    print(colours_list.index("Red"))
    #Return the number of times 'x' appear in the list
    colours_list=["Red", "Blue", "Green", "Black", "Blue"]
    colours_list.count("Blue")  
    #Sort the items of the list in place(Reversing alphabetically
    #(reverse = False is alphabatically ascending))
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list.sort(key=None, reverse=False)
    print(colours_list)
    #Reverse the elements of the list in place(just reversed first and last)
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list.reverse()
    print(colours_list)
    #Reverse a list
    even = [2,4,6,8]
    even.sort(reverse = True)
    print(even)
    #Return a shallow copy of the list
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list.copy()
    print(colours_list)
    #Lists are Mutable(change any item in the list)
    colours_list = ['Yellow', 'Red', 'Blue', 'Green', 'Black']
    colours_list[2] = "Pink"
    print(colours_list)
    #Convert a list to a tuple 
    list = [1,2,3,4,5]
    tuple = tuple(list)
    print(tuple)
    #use of the START:STOP:STEP in a list
    list = [1,2,3,4,5,6,7,8,9,10]
    print(list[3:9:2])
    print(list[6:4:2])
    #Find the largest and the smallest item in a list
    list = [1,2,3,4,5,6,7,8,9,10]
    print(max(list))
    print(min(list))
    #Compare two lists in Python
    list1, list2=[3, 5, 7, 9], [3, 5, 7, 9]
    print(list1 == list2)
    list1, list2=[3, 5, 7, 9, 8], [3, 5, 7, 9, 4]
    print(list1 == list2)
    #
    list1, list2=[3, 5, 7, 9], [3, 5, 7, 9]
    if list1 ==list2:
        print("The lists are equal")
    
    #order and compare
    print(list1.sort() == list2.sort())
    #print the indexing of the list
    list1 = ['H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D']
    index =list1.index('L')
    print(index)
    ##define the index from which you want to search
    index = list1.index("L", 4)
    print(index)
    ##define the segment of the list to be searched
    index = list1.index("O", 3, 5)
    print(index)
    #Using Lists as Stacks
    color_list=["Red", "Blue", "Green", "Black"]
    print(color_list)
    color_list.append("White")
    color_list.append("Yellow")
    print(color_list)
    color_list.pop()
    color_list.pop()
    color_list.pop()
    color_list
    
    #%%
    #Dictionary
    #(EMPTY DICTIONARY)
    new_dict = dict()
    print(new_dict)
    new_dict = {}
    print(new_dict)
        #Dictionary with key-vlaue
    colour = {"key1":"red","key2":"green","key3":"blue","key4":"white","key5":"black"} 
    print(colour)
    #Get value by key in Python dictionary
    colour = {"key1":"red","key2":"green","key3":"blue","key4":"white","key5":"black"}
    colour["key1"]
    colour["key5"]
    colour["key2"]
    #Adding a new value to a dictionary
    colour = {"key1":"red","key2":"green"}
    colour["key3"] = ("Black")
    colour
    number = {1:22.55,2:55.89,3:60.21}
    number[4]=61.08
    number
    ## update() method to add key-values
    number = {1:22.55,2:55.89,3:60.21}
    number.update({4:60.19})
    number
    number = {'a':22.55,'b':55.89,'c':60.21}
    number.update({'d':58.98})
    number
    #Iterating Python dictionaries using for loops
    dict = {"a":1,"b":2,"c":3,"d":4}
    for dict_key, value in dict.items():
        print(dict_key, ' represent ', dict[dict_key])
    #2
    colour = {"a":"red","b":"green","c":"blue"}
    for colour_key,value in colour.items():
        print (colour_key, 'corresponds to',colour[colour_key])
    #3
    dict = {"a":"Arjun","b":"Aryan","c":"Arnab","d":"Arif"}
    for dict_key, value in dict.items():
        print(dict_key, 'corresponds to ', dict[dict_key])
    #4
    dict = {"a":"Prob","b":"Prod","c":"Prof","a":"Prom"}    
    for dict_key, value in dict.items():
        print(dict_key , 'represents the begining of a word ', dict[dict_key])
    #Remove a key from a Python dictionary
    dict = {"a":1,"b":2,"c":3,"d":4}
    if 'a' in dict:
        del dict['a']
        print(dict)
    if 'b' in dict:
        del dict['b']
        print(dict)
    if 'c' in dict:
        del dict['c']
        print(dict)
    # sort dictionary by key
    color_dict = {'red':'#FF0000',
              'green':'#008000',
              'black':'#000000',
              'white':'#FFFFFF'}
    for key in sorted(color_dict):
        print("%s: %s" % (key,color_dict[key]))
    #finding a max and min value in dictionary
    my_dict = {'x':500, 'y':5874, 'z': 560}
    key_max = max(my_dict.keys(), key = (lambda k: my_dict[k]))
    key_min = min(my_dict.keys(), key = (lambda k: my_dict[k]))
    print('Maximum value: ', my_dict[key_max])
    print('Minimum value: ', my_dict[key_min])
    #Concatenate two Python dictionaries into a new one
    dict1 = {1:10,2:20}
    dict2 = {4:40,5:20}  
    dict3 = {}
    for d in (dict1, dict2): dict3.update(d)
    print(dict3)
    #
    dict1 = {'a':20,'b':50}
    dict2 = {'c':25,'d':30}
    dict3 = {}
    for d in (dict1,dict2): dict3.update(d)
    print(dict3)
    #
    dict1 = {"key1":"Orange","key2":"Purple"}
    dict2 = {"key3":"Brown","key4":"White"}
    dict3 = {}
    for d in (dict1,dict2): dict3.update(d)
    print(dict3)
    #Find the length of a Python dictionary
    dict1 = {"key1":"Orange","key2":"Purple"}
    print(len(dict1))
    dict2 = {"key3":"Brown","key4":"White"}
    print(len(dict2))
    #%%
    #Tuple
    #empty tuple
    tuple = ()
    print(tuple)
    ##create a tuple with different data types
    tuple1 = ('tuple', False, 3.2, 1)
    print(tuple1)
    ##create a tuple with numbers, notation without parenthesis
    tuple2 = 1,2,3,4,5,6
    print(tuple2)
    ##create a tuple of one item, notation without parenthesis
    tuple4 = 4,
    print(tuple4)
    ##create a tuple from a iterable object
    tuple5 = ([True,False])
    print(tuple5)
    #get item from a tuple(first,last,middle)
    tuple6 = ("w", 3, "r", "e", "s", "o", "u", "r", "c", "e") 
    tuple6[3]
    tuple6[5]
    tuple6[-4]
    tuple6[-6]
    # know if an element exists within a tuple
    tuple6 = ("w", 3, "r", "e", "s", "o", "u", "r", "c", "e") 
    print("r" in tuple6)
    print("o" in tuple6)
    print("z" in tuple6)
    print(5 in tuple6)
    #conversion of List to tuple
    #lst = [1,2,3,4,5,6]
    #tup = tuple(lst)
    #print(tup)
    #Add item in Python tuple
    #using merge of tuples with the + operator you can add an element and 
    #it will create a new tuple
    tuple = (1,2,3,4,5,6)
    tuple1 = tuple+(7,)
    print(tuple1)
    ##adding items in a specific index
    tuple = (1,2,3,4,5,6)
    tuple1 = tuple[:4] + (15, 20, 25, 30, 35) + tuple[:5]
    print(tuple1)
    #
    tuple = (1,2,3,4,5,6)
    tuple1 = tuple[:2] + (3,4,5,6,7,8,9) + tuple[:-5]
    print(tuple1)
    #
    tuple = (1,2,3,4,5,6,7,8,9)
    tuple1 = tuple[:6] + (11,12,13,14,15,16,17,18)+ tuple[:-2]+(1,2,3)
    print(tuple1)
    #return the number of times it appears in the tuple.
    tuple = 2, 4, 5, 6, 2, 3, 4, 4, 7 
    count = tuple.count(4)
    print(count)
    #
    tuple = (1, 2, 3, 4, 5, 6, 11, 12, 13, 14, 15, 16, 17, 18, 1, 2, 3, 4, 5, 6, 7, 1, 2, 3)
    count = tuple.count(1)
    print(count)
    count = tuple.count(2)
    print(count)
    count = tuple.count(3)
    print(count)
    #Remove an item from a tuple
    ##using merge of tuples with the + operator you can remove an item and it will 
    #create a new tuple,Below example "d" is removed
    tuple = ("w", 3, "d", "r", "e", "s", "l")
    tuple1 = tuple[:2] + tuple[3:]
    print(tuple1)
    #Slicing a tuple
    tuple = (2, 4, 3, 5, 4, 6, 7, 8, 6, 1)
    _slice1 = tuple[2:5]
    print(_slice1)
    _slice2 = tuple[:6]
    print(_slice2)
    _slice3 = tuple[:-6]
    print(_slice3)
    _slice4 = tuple[-8:-4] 
    >>> print(_slice4)
    #Find the index of an item of the tuple
    tuple = (2, 4, 3, 5, 4, 6, 7, 8, 6, 1)
    print(tuple.index(8))
    print(tuple.index(5)) 
    #
    tuple = ('i', 'n', 'd', 'e', 'x', ' ', 't', 'u', 'p', 'l', 'e')
    index = tuple.index('x')
    print(index)
    index = tuple.index('p', 5)
    print(index)
    ##define the segment of the tuple to be searched
    index = tuple.index("e", 3, 6) 
    print(index)
    #The size of a tuple
    tuple = (2, 4, 3, 5, 4, 6, 7, 8, 6, 1)
    print(len(tuple))
    #Slice of a tuple using step parameter
    tuple = ('H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D')
    #tuple[start:stop:step]
    _slice = tuple[2:9:2]
    print(_slice)	
    #Modify items of a tuple
    tuple = ("w", 3, "r", [], False)
    # #tuples are immutable, so you can not modify items which are also immutable,
    # as str, boolean, numbers etc.
    tuple[3].append(200)
    print(tuple)
    tuple = ('H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D')
    tuple[5].append('Q')
    print(tuple)
    #Iterators and iterable objects
    string = "1234567890"
    for char in string:
        print(char)
    #
    string = "1234567890"
    for char in iter(string):
        print(char)
    #using for loop
    my_list = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]
    my_iterator = iter(my_list)
    for i in range(0,len(my_list)):
        next_item = next(my_iterator)
        print(next_item)
    #043 Understanding and using Ranges
    print(range(100))
    my_list = list(range(10))
    print(my_list)
    #using START:STOP:STEP
    even = list(range(0,100,2))
    odd = list(range(1,100,2))
    print(even)
    print(odd)
    #Range does't support all the operations like mode,concartenation(append)
    small_decimals = range(0,10)
    print(small_decimals)
    print(small_decimals.index(3))
    # to see the 'ODD' number in a range
    odd = range(1, 1000, 2)
    print(odd)
    #
    seven = range(7, 100000, 7)
    x = int(input("please a number less than one million : "))
    if x in seven:
        print("{} is divisible by seven".format(x))
    #
    my_range = small_decimals[::2]
    print(my_range)
    print(my_range.index[4])
    #
    decimals = range(0,100)
    my_range = decimals[3:40:3]
    print(my_range)
    for i in my_range:
        print(i)
    #True False check
    print(range(0, 5, 2)) == print(range(0, 6, 2))
    #why it happened like this ,let's see...it gives the same value 
    print(list(range(0, 5, 2)))
    print(list(range(0, 6, 2)))
    #
    r = range(0,100)
    for i in r:
        print(i)
    r = range(0,99)
    for i in r:
        print(i)
    #
    r = range(0, 10)
    for i in r[::-1]:
        print(i)
    #
     o = range(0, 100, 4)
     print(o)
     p = o[::5]
     for i in p:
         print(i)
    #%%
    #026 An Introduction To Program Flow Control
    for i in range(1, 12):
        print(i)
    #
    for i in range(1, 12):
        print("no {} squared is {} and cube is {:4}".format(i, i**2, i**4))
        #027 Test Conditions With If ElIf  Else
    name = input("Please enter your name: ")
    age = input("How old are you, {}?".format(name))
    print(age)
    #now we can change the data type in "age" as an integer
    name = input("Please enter your name: ")
    age = int(input("How old are you, {}?".format(name)))
    print(age)
    #
    if age >= 18:
        print("you are old enough to vote")
    else:
        print("Please come back in {0} years".format(18-age))
    #
    #Use the in operator in an if statement
    s = 'jQuery'
    #create a list
    l = ['JavaScript', 'jQuery', 'ZinoUI']
    # in operator is used to replace various expressions that use the or operator
    if s in l:
        print(s + ' Tutorial')
    #Alternate if statement with or operator
    if s == 'JavaScript' or s == 'jQuery' or s == 'ZinoUI':
         print(s + ' Tutorial')
    #
    a=10
    if(a>10):
        print("Value of a is greater than 10")
    else :
        print("Value of a is 10")
    #
    x = 1+2j
    if (type(x) == int):
        print("variable is an integer")
    elif (type(x) == float):
        print("variable is an float")
    elif (type(x) == dict):
        print("variable is an dictionaries")
    elif (type(x) == complex):
        print("variable is an complex")
    elif (type(x) == bool):
        print("variable is an bool")
    elif (type(x) == string):
        print("variable is an string")
    elif (type(x) == tuple):
        print("variable is an tuple")
    elif (type(x) == list):
        print("variable is an list")
    else:
        print("Type is unknown")
    #
    age = 25
    if (age>=10):
        print("You are eligible to see")
        if (age <= 20 or age >= 60):
            print("Ticket price is 1000")
        else:
            print("Ticket price is 1500")
    else:
        print("Better luck next time")
     #
    #Use the and operator in an if statement
    x = False
    y = True
    if x and y:
        print('Both x and y are True')
    else:
        print('x is False or y is False or both x and y are False')
     #
    #Write an if-else in a single line of code
    n = 150
    print(n)
    #if n is greater than 500, n is multiplied by 7, otherwise n is divided by 7
    result = n * 7 if n > 500 else n / 7
    print(result)
    #
    #Define a negative if
    x = 20
    print(x)
    #uses the not operator to reverse the result of the logical expression
    if not x == 50:
        print('the value of x different from 50')
    else:
        print('the value of x is equal to 50')
    #
    print("Please guess a number between 0 and 10 :")
    guess = int(input())
    if guess <5:
        print("Print guess higher")
        guess = int(input())
        if guess ==5:
            print("You guessed it correctly")
        else:
            print("Please choose a higher number")
    elif guess >5:
        print("Please guess it lower")
        if guess == 5:
            print("You guessed it correctly")
        else:
            print("Please choose a higher number")
    else:
        print("you got it right first time")
    #FOR LOOP
    color_list = ["Red", "Blue", "Green", "Black"]
    for c in color_list:
        print(c)
    #
    for a in range(4):
      print(a)
    for a in range(2,7):
     print(a)
    for a in range(2,19,5):
      print(a)
    for i in range(0,100,10):
        print("i is {}".format(i))
    for i in range(1,13):
        for j in range(1,13):
            print("{1} times {0} is {2}".format(i, j, i*j),end='\t')
        print("===============")
    #
    numbers = (1, 2, 3, 4, 5, 6, 7, 8, 9)
    count_even = 0
    count_odd = 0
    for x in numbers:
        if x %2:
            count_odd+=1
        else:
            count_even+=1
    print("Number of even numbers :",count_even)
    print("Number of odd numbers :",count_odd)
    #
    datalist = [1452, 11.23, 1+2j, True, 'w3resource', (0, -1), [5, 12],
    {"class":'V', "section":'A'}]
    for item in datalist:
       print ("Type of ",item, " is ", type(item))
    #
    color = {"c1": "Red", "c2": "Green", "c3": "Orange"}
    for key in color:
        print(key)
    #
    color = {"c1": "Red", "c2": "Green", "c3": "Orange"}
    for value in color.values():
        print(value)
    #031 Extending For Loops
    number = "9,223,372,036,854,775,807"
    cleanedNumber = ''
    for char in number:
        if char in '0123456789':
            cleanedNumber = cleanedNumber + char
    newNumber = int(cleanedNumber)
    print("The number is {}".format(newNumber))
    #
    number = "111,221,31,478,511,675,714,878,992"
    cleanedNumber = ''
    for char in number:
        if char in '0123456789':
            cleanedNumber = cleanedNumber + char
    newNumber = int(cleanedNumber)
    print("The number is {}".format(newNumber))
    #
    #this is same as print("The asian country is {}"+country)
    for country in ["India","China","Japan","Israel","Jordan","Cyprus","Cambodia","Brunei"]:
        #print("The asian country is " + country)
        #print("The asian country is {}".format(country))
    #
    #While loop
    x = 0;
    while x <5:
        print(x)
        x+=1
    #Look the example as it will display no RETURN
    x = 10;
    while x <5:
        print(x)
        x+=1   
    #
    x = 0;
    s = 0
    while (x < 10):
         s = s + x
         x = x + 1
    else :
         print('The sum of first 9 integers : ',s)
    #while loop with if-else and break statement
    x = 1;
    s = 0
    while (x < 10):
         s = s + x
         x = x + 1
         if (x == 5):
              break
    else :
         print('The sum of first 9 integers : ',s)        
    print('The sum of ',x,' numbers is :',s) 
    #032 Understanding Continue Break And Else
    shopping_list = ["Milk","Vegetable","Pasta","Egg","Bread"]
    for i in shopping_list:
        if i == "Milk":
         continue
         #break
        print("Buy"+ i)
    #
    for letter in 'python':
        if letter == 'y':
            break
        print('Current letter:',letter)
    #else:
        #print('letter')
    #
    var = 10
    while var > 0:
        var = var -1
        if var == 5:
            continue
        print('current value:', var)
    print('Good Bye !')
    #
    for num in range(10,20):
    #to iterate between 10 to 20
       for i in range(2,num): 
    #to iterate on the factors of the number
          if num%i == 0:      
    #to determine the first factor
             j=num/i 
    #to calculate the second factor
             print '%d equals %d * %d' % (num,i,j)
             break 
    #to move to the next number, the #first FOR
       else:        
    # else part of the loop
          print num, 'is a prime number'     
    #for num in range(10,20):
    #   for i in range(2,num):
    #      if num%1 ==0:
    #         j=num/i
    #         print ('%d equals %d * %d' %(num,i,j))
    #         break
    #   else:
    #       print(num , 'is a prime number')
    #033 Augmented Assignment
    number = "9,223,372,036,854,775,807"
    cleanedNumber = ''       
    for i in range(0, len(number)):
        if number [i] in '0123456789':
            cleanedNumber += number[i]
            new_number = int(cleanedNumber)
            print("the number is {} ".format(new_number))
    #
    x = 23
    x+=1
    print(x)
    #
    x = 24
    x-=1
    print(x)
    #
    x = 55
    x/=5
    print(x)
    #
    x = 25
    x*=4
    print(x)
    #
    x**=4
    print(x)
    #
    x %=60
    print(x)
    #
    greeting = "Good"
    greeting += "Morning"
    print(greeting)
    #048 Binary Basics,049 What is binary
    #
    #
    # Input and Output (IO) in Python
    file = open("C:\\Users\\Manas\\Desktop\\sample.txt",'r')
    for line in file:
        print(line)
    #with general statement
    file = open("C:\\Users\\Manas\\Desktop\\sample.txt")
    data = file.read()
    print(data)
    #now by using "with"
    with open ("C:\\Users\\Manas\\Desktop\\sample.txt") as file
    data = file.read()
    print(data)
    #converting all the lines in the text to lower case
    with open("C:\\Users\\Manas\\Desktop\\sample.txt") as file:
        for line in file:
            line = line.lower()
            print(line)
    #converting all te lines in the text file as upper case
    file = open("C:\\Users\\Manas\\Desktop\\sample.txt")
    data = file.read()
    print(data)
    for line in data:
        lines = line.upper()
        print(lines)
      
    
                 
    
    
    
    
    
    
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
