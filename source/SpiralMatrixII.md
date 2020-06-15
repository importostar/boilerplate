---
title: SpiralMatrixII
date: 2020-05-07
---
Example Python program SpiralMatrixII.py


## Classes

* class Solution:

## Methods

* def generateMatrix(self, n):

## Code

Python example

    """
    Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.
    
    For example,
    Given n = 3,
    
    You should return the following matrix:
    [
     [ 1, 2, 3 ],
     [ 8, 9, 4 ],
     [ 7, 6, 5 ]
    ]
    """
    class Solution:
        # @return a list of lists of integer
        def generateMatrix(self, n):
            if n<=0:
                return [] 
    
            # row[:] mean shallow copy each row in [[0]*n]*n
            # we cannot not use row replace row[:] here 
            matrix=[row[:] for row in [[0]*n]*n]
            
            row_st=0
            row_ed=n-1
            
            col_st=0
            col_ed=n-1
            current=1
            
            while (True):
                if current>n*n:
                    break
                for c in range (col_st, col_ed+1):
                    matrix[row_st][c]=current
                    current+=1
                row_st+=1
                for r in range (row_st, row_ed+1):
                    matrix[r][col_ed]=current
                    current+=1
                col_ed-=1
                for c in range (col_ed, col_st-1, -1):
                    matrix[row_ed][c]=current
                    current+=1
                row_ed-=1
                for r in range (row_ed, row_st-1, -1):
                    matrix[r][col_st]=current
                    current+=1
                col_st+=1
            return matrix

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
