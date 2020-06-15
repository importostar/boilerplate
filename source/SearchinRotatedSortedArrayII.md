---
title: SearchinRotatedSortedArrayII
date: 2020-05-07
---
Example Python program SearchinRotatedSortedArrayII.py


## Classes

* class Solution:

## Methods

* def search(self, A, target):
* def searchHelper(self, A, target, start, end):

## Code

Python example

    class Solution:
        # @param A a list of integers
        # @param target an integer
        # @return a boolean
        def search(self, A, target):
            if A==None or len(A)==0:
                return False
            start=0;
            end=len(A)-1
            
            if self.searchHelper(A, target, start, end)==1:
                return True
            else:
                return False
                
        def searchHelper(self, A, target, start, end):
            if start>end:
                return -1
            mid=(start+end)/2
            
            if A[mid]==target:
                return 1
                
            if A[start]<A[mid]:
                if A[start]<=target<=A[mid]:
                    return self.searchHelper(A, target, start, mid)
                else:
                    return self.searchHelper(A, target, mid+1, end)
            elif A[start]>A[mid]:
                if A[mid]<=target<=A[end]:
                    return self.searchHelper(A, target, mid, end)
                else:
                    return self.searchHelper(A, target, start, mid-1)
            else:
                if A[mid]!=A[end]:
                    return self.searchHelper(A, target, mid+1, end)
                            
                else:
                    left=self.searchHelper(A, target, start, mid-1)
                    if left!=-1:
                        return left
                    else:
                        return self.searchHelper(A, target, mid+1, end-1)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
