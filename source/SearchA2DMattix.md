---
title: SearchA2DMattix
date: 2020-05-07
---
Example Python program SearchA2DMattix.py


## Classes

* class Solution:

## Methods

* def searchMatrix(self, matrix, target):

## Code

Python example

    """
    Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
    
    Integers in each row are sorted from left to right.
    The first integer of each row is greater than the last integer of the previous row.
    For example,
    
    Consider the following matrix:
    
    [
      [1,   3,  5,  7],
      [10, 11, 16, 20],
      [23, 30, 34, 50]
    ]
    Given target = 3, return true.
    """
    
    class Solution:
        # @param matrix, a list of lists of integers
        # @param target, an integer
        # @return a boolean
        def searchMatrix(self, matrix, target):
            if matrix==None or len(matrix)==0:
                return False
                
            start=0
            end=len(matrix)*len(matrix[0])-1
                
            while (start<=end):
                mid=start+(end-start)/2
                    
                if matrix[mid/len(matrix[0])][mid%len(matrix[0])]==target:
                    return True
                    
                elif matrix[mid/len(matrix[0])][mid%len(matrix[0])]<target:
                    start=mid+1
                else:
                    end=mid-1
                
            return False

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
