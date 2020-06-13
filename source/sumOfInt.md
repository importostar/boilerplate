---
title: sumOfInt
date: 2020-05-07
---
Example Python program sumOfInt.py


## Methods

* def sumOfInt(lb,ub):
*   def sumOfSquareOfInt(lb,ub):
*   def sumOfCubeOfInt(lb,ub):
* def sumOfInts(f, lb, ub):
* def sumOfInts(f, lb, ub):

## Code

Python example

    lb=0
    ub=100
    def sumOfInt(lb,ub):
      total = 0
      for i in range(lb,ub + 1):
        total = total + i
      return total  
      
      # Traditional way to do square of sum of Integers
      def sumOfSquareOfInt(lb,ub):
        total = 0
        for i in range(lb,ub):
          total = total + (i * i)
        return total
      
      # Traditional way to do cube of sum of Integers
      def sumOfCubeOfInt(lb,ub):
        total = 0
        for i in range(lb,ub):
          total = total + (i * i * i)
        return total
        
        # Anonymous frunction or lamda function. Every thing remains same as in the firat function sumOfInt()
        def sumOfInts(f, lb, ub):
          total = 0
          for i in range(lb, ub + 1):
            total = total + f(i)     # The f(i) part is unknown and a function is passed as f and invokes f(i) with one argument
          return total
        
        sumOfInts(lambda i: i, 1,100)     # Anonymous function (functionality with no name) is passed using lambda keyword 
        sumOfInts(lambda i: i*i*i, 1,100) # cube of Ints
        sumOfInts(lambda i: i*i, 1,100)   # square of Ints
        sumOfInts(lambda i: i*2, 1,100)   # integer multiply by 2
        
        # sumOfInt with two Arguments
        def sumOfInts(f, lb, ub):
          total = 0
          c = 2
          for i in range(lb, ub + 1):
            total = total + f(i, c)
          return  total
        
        sumOfInts(lambda i,c: i+c, 1, 100)  # i+c is the functionality for f(i, c) the 2 arguments passed
        
        # sumOfInt only if they are even else just leave them
        sumOfInts(lambda i: i if(i%2 == 0) else 0 ,1 , 100)
        
        #List is a collection in python
        #Range is a special kind of list in python. To conver range to list to following
        l = list(range(1,101))
        
        # To access the list element
        l[0]
        l[1]
        l[:5]
        l[-5]
        l.count(1) # to find how many times 1 been repeated in the list l
        l.sort()
        l.pop(0) # to delete
        l.indexOf(6)  # to find where 6 is
        l.indexOf(2,6) # find on which index 6 is starting from index 2
        l.append(101)
        l.reverse()
        
        help(l)
        
        
        
        # Set --> cant have duplicates - rest all similiar to list
        set(l)  # duplicates will be eliminated
        
        # To open a file in python
        orderItems = open("c:\\retail_db\\order_items\\part-00000")
        type(orderItems) # file 
        orderItems = open("c:\\retail_db\\order_items\\part-00000").read()
        type(orderItems)  #str
        orderItems = open("c:\\retail_db\\order_items\\part-00000").readlines() #retrun collection of str with \n with each element
        
        # to avoid it use read().splitlines()
        orderItems = open("c:\\retail_db\\order_items\\part-00000").read().splitlines() # no \n in the array of elements
        orderItems[:5]
        len(orderItems)
        
        # Find a file in linux
        find . -name "*.tsv" -type f/d   # file for file / d  for directory
        find . -name "*.tsv" -type f | wc -l
        
        #Dict -- {Key Value} Pair collection
        d = {1 : "Scott", 2 : "Jay"}
        d[3]="Tiger"    # to append new key value pair
        d[2]="Woods"    # will replace "Jay" with "Woods"
        d.get(1)        # Scott
        d.has_key(1)    # returns true or false
        d.items()       # create collection out of it
        d.iterkeys()    # to get only the keys
        d.itervalues()  # to get only the values
      

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
