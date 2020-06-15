---
title: pengxiang_hua_data_lake_similarity_filter_verificate_verify
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_verify.py


## Methods

* def verify(r, s, t, olap, pr , ps):

## Code

Python example

    '''
    from PVLDB'16-An Empirical Evaluation of Set Similarity Join Techniques
         Algorithm 1: Verify(r; s; t; olap; pr ; ps)
    '''
    def verify(r, s, t, olap, pr , ps):
        '''
        :param r: set
        :param s: set
        :param t: required overlap
        :param olap,pr,ps: overlap up to positions pr ,ps in r,s
        :param order:dict word2df
        :return: true if |r∩s|≥t, i.e., (r,s) is in the result set
        '''
        maxr = len(r)- pr + olap
        maxs = len(s)- ps + olap
        while t <= maxr and t <= maxs and t > olap:
            if r[pr] == s[ps]:
                pr += 1
                ps += 1
                olap += 1
            elif r[pr] < s[ps]:
                pr += 1
                maxr -= 1
            else:
                ps += 1
                maxs -= 1
        return olap >= t,olap

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
