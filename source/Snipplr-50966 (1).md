---
title: Snipplr 50966 (1)
date: 2020-05-07
---
Example Python program Snipplr-50966 (1).py

## Modules

* import csv
* import sys
* import csv
* import sys

## Code

Python example

    # Use reader() to create a an object for reading data from a CSV file. The reader can be used as an iterator
    #  to process the rows of the file in order. For example:	
    
    import csv
    import sys
    
    f = open(sys.argv[1], 'rt')
    try:
        reader = csv.reader(f)
        for row in reader:
            print row
    finally:
        f.close()
    
    
    # the original file:
    
    "Title 1","Title 2","Title 3"
    1,"a",08/18/07
    2,"b",08/19/07
    3,"c",08/20/07
    4,"d",08/21/07
    5,"e",08/22/07
    6,"f",08/23/07
    7,"g",08/24/07
    8,"h",08/25/07
    9,"i",08/26/07
    
    
    # the result:
    
    $ python csv_reader.py testdata.csv
    
    ['Title 1', 'Title 2', 'Title 3']
    ['1', 'a', '08/18/07']
    ['2', 'b', '08/19/07']
    ['3', 'c', '08/20/07']
    ['4', 'd', '08/21/07']
    ['5', 'e', '08/22/07']
    ['6', 'f', '08/23/07']
    ['7', 'g', '08/24/07']
    ['8', 'h', '08/25/07']
    ['9', 'i', '08/26/07']
    
    
    
    
    
    
    
    # In addition to working with sequences of data, the csv module includes classes for working  # with rows as dictionaries so that the fields can be named. The DictReader and DictWriter # #  classes translate rows to dictionaries instead of lists. Keys for the dictionary can be # #  passed in, or inferred from the first row in the input (when the row contains headers).
    
    
    
    import csv
    import sys
    
    f = open(sys.argv[1], 'rt')
    try:
        reader = csv.DictReader(f)
        for row in reader:
            print row
    finally:
        f.close()
    
    
    # returns:
    
    
    $ python csv_dictreader.py testdata.csv
    
    {'Title 1': '1', 'Title 3': '08/18/07', 'Title 2': 'a'}
    {'Title 1': '2', 'Title 3': '08/19/07', 'Title 2': 'b'}
    {'Title 1': '3', 'Title 3': '08/20/07', 'Title 2': 'c'}
    {'Title 1': '4', 'Title 3': '08/21/07', 'Title 2': 'd'}
    {'Title 1': '5', 'Title 3': '08/22/07', 'Title 2': 'e'}
    {'Title 1': '6', 'Title 3': '08/23/07', 'Title 2': 'f'}
    {'Title 1': '7', 'Title 3': '08/24/07', 'Title 2': 'g'}
    {'Title 1': '8', 'Title 3': '08/25/07', 'Title 2': 'h'}
    {'Title 1': '9', 'Title 3': '08/26/07', 'Title 2': 'i'}

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
