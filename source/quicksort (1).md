---
title: quicksort (1)
date: 2020-05-07
---
Example Python program quicksort (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def quicksort1(q):
* def quicksort2(q):
* def quicksort_in_place(q, left, right):
* def partition(q, left, right, pivotIndex):
* def swap(q, i, j):
* def main():

## Code

Python example

    #!/usr/bin/env python
    
    def quicksort1(q):
        """
        The basic version.
        http://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F#.E6.BC.94.E7.AE.97.E6.B3.95
        """
        less = []
        pivotList = []
        greater = []
    
        length = len(q)
        if length <= 1:
            return q
        else:
            pivotIndex = length / 2 - 1;
            pivot = q[pivotIndex]
            i = -1
            for x in q:
                i += 1
                if i == pivotIndex:
                    continue
                if x < pivot:
                    less.append(x)
                else:
                    greater.append(x)
            pivotList.append(pivot)
            return quicksort1(less) + pivotList + quicksort1(greater)
    
    def quicksort2(q):
        """
        The complex version, use in-place partition algorithm, more effective.
        http://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F#.E5.8E.9F.E5.9C.B0.28in-place.29.E5.88.86.E5.89.B2.E7.9A.84.E7.89.88.E6.9C.AC
        """
        quicksort_in_place(q, 0, len(q)-1)
        return q
    
    def quicksort_in_place(q, left, right):
        if left < right:
            pivotIndex = (left + right) / 2
            pivotNewIndex = partition(q, left, right, pivotIndex)
            quicksort_in_place(q, left, pivotNewIndex - 1)
            quicksort_in_place(q, pivotNewIndex + 1, right)
    
    def partition(q, left, right, pivotIndex):
        pivot = q[pivotIndex]
        swap(q, pivotIndex, right)
        storeIndex = left
        i = left
        for x in q[left:right]:
            if x < pivot:
                swap(q, i, storeIndex)
                storeIndex += 1
            i += 1
        swap(q, storeIndex, right)
        return storeIndex
    
    def swap(q, i, j):
        temp = q[i]
        q[i] = q[j]
        q[j] = temp
    
    #test
    def main():
        # quicksort1
        print(quicksort1([3,87,9,7,43,57,3,2,2,73]))
    
        # quicksort2
        print(quicksort2([3,87,9,7,43,57,3,2,2,73]))
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
