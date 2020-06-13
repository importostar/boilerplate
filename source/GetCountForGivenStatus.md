---
title: GetCountForGivenStatus
date: 2020-05-07
---
Example Python program GetCountForGivenStatus.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys  # its make ur program capable of accepting arguments & argv[] to read arguments
* import sys

## Methods

* def getCountForGivenStatus(orders, status):
* def getCountForStudInSocial(stud, social):
* def getCountForStudInSocial(stud,social):

## Code

Python example

    #Using retail_db
    orders = open("dataPath/retail_db/orders/part*").read().splitlines()
    len(orders)
    type(orders)
    orders[0]    # '1,2013-07-25 00:00:00.0,11599,CLOSED'
    
    orderMap = map(lambda rec: rec.split(",")[3], orders)
    
    def getCountForGivenStatus(orders, status):
      ordersFiltered = filter(lambda rec: rec.split(",")[3] == status, orders)
      return len(ordersFiltered)
    
    getCountForGivenStatus(orders,'COMPLETE')
    
    ---------------------
    import sys      # its make ur program capable of accepting arguments & argv[] to read arguments
    def getCountForStudInSocial(stud, social):
      count = 0
      for s in stud:
        if (social in s.split("\t")[7].split(",")):
          count = count +1
      return count  
    
    stud = open("data/Path/stud.tsv").read().splitlines()
    print("Running " +sys.argv[0])
    print(getCountForStudInSocial(stud,sys.argv[1]))
    
    # save the above code in a file like social.py then from the prompt run it this way
    python social.py dataPath/retail_db/orders/part* Google
    
    # Above code written with improvement
    import sys
    def getCountForStudInSocial(stud,social):
      counnt = 0
      for s in stud:
        if(social in s.split("\t")[7].split(",")):
          count = count + 1
      return count
    
    stud = open(sys.argv[1]).read().splitlines()
    print("Running " +sys.argv[0])
    social = sys.argv[2]
    print("Number of Students using " +social +" "+ str(getCountForStudInSocial(stud,social)))
    # To execute
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
