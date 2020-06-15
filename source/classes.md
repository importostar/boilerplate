---
title: classes
date: 2020-05-07
---
Example Python program classes.py
For Python version 2.x.
To test your Python version use:

    python --version


## Classes

* class space:
* class area:
* class square(area):

## Methods

* def __init__(self, spacename, column, row, value):
* def make_impossible(self, value):
* def __init__(self, name):
* def make_impossible(self, value):
* def set_columns_and_rows(self):

## Code

Python example

    class space:
        def __init__(self, spacename, column, row, value):
            self.name = spacename
            self.value = value
            self.row = str(row)
            self.column = column
            self.impossible = []
            if self.value == 0:
                self.possible = [1,2,3,4,5,6,7,8,9]
            else:
                self.possible = self.value
    
        def make_impossible(self, value):
            if type(self.possible) == list:
                if value in self.possible:
                    self.possible.remove(value)
            if value not in self.impossible:
                self.impossible.append(value)
    class area:
        def __init__(self, name):
            self.name = name
            self.need = [1,2,3,4,5,6,7,8,9]
            self.impossible = []
    
        def make_impossible(self, value):
            if value in self.need:
                self.need.remove(value)
            if value not in self.impossible:
                self.impossible.append(value)
    
    class square(area):
        def set_columns_and_rows(self):        
                 
            left_columns = ["A", "B", "C"]
            center_columns = ["D", "E", "F"]
            right_columns = ["G", "H", "I"]
            
            top_rows = ["1","2","3"]
            middle_rows = ["4","5","6"]
            bottom_rows = ["7","8","9"]
            
            if self.name[-1] == "1":
                self.columns = left_columns
                self.rows = top_rows
                
            elif self.name[-1] == "2":
                self.columns = center_columns
                self.rows = top_rows
                
            elif self.name[-1] == "3":
                self.columns = right_columns
                self.rows = top_rows
                
            elif self.name[-1] == "4":
                self.columns = left_columns
                self.rows = middle_rows
                
            elif self.name[-1] == "5":
                self.columns = center_columns
                self.rows = middle_rows
                
            elif self.name[-1] == "6":
                self.columns = right_columns
                self.rows = middle_rows
                
            elif self.name[-1] == "7":
                self.columns = left_columns
                self.rows = bottom_rows
          
            elif self.name[-1] == "8":
                self.columns = center_columns
                self.rows = bottom_rows
         
            elif self.name[-1] == "9":
                self.columns = right_columns
                self.rows = bottom_rows
            else:
                print "how"
    
                

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
