---
title: bm
date: 2020-05-07
---
Example Python program bm.py


## Methods

* def find_boyer_moore(T, P):
* def find_boyer_moore2(T, P):

## Code

Python example

    """
    Pattern matching problem
    Boyer Moore algorithm
    
    First is my attempt, below is the code provided in the book
    Idea:
    Optimize brute force approach using 2 heuristics:
    - Looking-Glass: start searches from last character of the
    pattern and work backwards
    - Character-Jump: During testing of a pattern P, a mismatch
    in T[i] = c with corresponding pattern P[k] is handled:
    a) if C is not contained in P, shift P completely past i.
    b) if c is contained in P shift P until an occurrence of c
    gets aligned with T[i]
    
    """
    
    
    def find_boyer_moore(T, P):
        """ return lowest index of T at which the substring P begins or -1"""
        n, m = len(T), len(P)
        if m == 0: return 0
        last = {}               # Using hash table for fast access
        for k in range(m):
            last[P[k]] = k
        i = m - 1           # i index at T, k index at P
        k = m - 1                    # j index of last occurrence of T[i] in P
        while i < n:
            if T[i] == P[k]:            # if chars are equal
                i -= 1                  # THIS
                k -= 1                  # THIS
                if k == 0:              # THIS
                    return i     # check if Patter is complete THIS
            else:
                # if j < k (remember k index at P)
                # shift i += m - (j+1)
                # if j > k
                # shift i += m - k
                j = last.get(T[i], -1)     # -1 if item not there
                i += m - (min(k, j+1))
                k = m - 1
        return -1
    
    
    def find_boyer_moore2(T, P):
        """ return lowest index of T at which the substring P begins or -1"""
        n, m = len(T), len(P)
        if m == 0: return 0
        last = {}               # Using hash table for fast access
        for k in range(m):
            last[P[k]] = k
        i = m - 1           # i index at T, k index at P
        k = m - 1                    # j index of last occurrence of T[i] in P
        while i < n:
            if T[i] == P[k]:            # if chars are equal
                if k == 0:
                    return i     # check if Patter is complete
                else:
                    i -= 1                  # normal iteration
                    k -= 1
            else:
                # if j < k (remember k index at P)
                # shift i += m - (j+1)
                # if j > k
                # shift i += m - k
                j = last.get(T[i], -1)     # -1 if item not there
                i += m - (min(k, j+1))
                k = m - 1
        return -1
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
