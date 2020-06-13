---
title: pengxiang_hua_data_lake_test_test2
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_test_test2.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import  struct

## Methods

* def find_first_gt_sk(list_t,sk,start,end):

## Code

Python example

    
    import  struct
    
    r = [1470796, 1567097, 1657623, 1742820, 1895994, 2060105, 2060106, 2089594, 2270727, 2270728, 2396070, 2414437, 2449826, 2482829, 2482830, 2498604, 2498605, 2528514, 2556134, 2594655, 2661345, 2671406, 2782754, 2807049, 2852578, 2861095, 2878801, 2943775, 2948013, 2964398, 2970763, 2970764, 2999016, 3004455]
    s = [1470796, 1567097, 1895994, 2060105, 2060106, 2089594, 2270728, 2315156, 2396070, 2449826, 2482829, 2482830, 2498604, 2498605, 2528514, 2556134, 2594655, 2661345, 2807049, 2852578, 2861095, 2878801, 2943775, 2948013, 2964398, 2970763, 2970764, 2999016, 3004455]
    
    
    def find_first_gt_sk(list_t,sk,start,end):
        left = start
        right = end
        while left < right:
            mid = (right-left)//2 + left
            if sk == list_t[mid]:
                while start <= mid - 1 < end and sk == list_t[mid - 1]:
                    mid -= 1
                return mid
            elif sk < list_t[mid]:
                right = mid - 1
            else:
                left = mid + 1
        while  right < len(list_t) and sk > list_t[right]:
            right += 1
        return min(right,len(list_t)-1)
    
    if __name__ == '__main__':
    
        r = [1]
        pos = find_first_gt_sk(r,3,0,len(r))
        print(pos,r[pos])
        t = r[:pos+1]
        s = r[pos+1:]
        print(t)
        print(s)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
