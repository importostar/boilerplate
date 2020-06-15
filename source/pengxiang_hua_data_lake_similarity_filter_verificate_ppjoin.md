---
title: pengxiang_hua_data_lake_similarity_filter_verificate_ppjoin
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_ppjoin.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import math
* from data_lake.similarity.filter_verificate.verify import verify
* from utlities.time_evaluate import *
* from utlities.statistics import *

## Methods

* def ppjoin(records,threshold):

## Code

Python example

    import math
    from data_lake.similarity.filter_verificate.verify import verify
    from utlities.time_evaluate import *
    from utlities.statistics import *
    
    @timer
    def ppjoin(records,threshold):
        '''
         WWW'08-Efficient similarity joins for near duplicate detection
        :param records:
        :param threshold:Jaccard
        :return:
        '''
        result = []
        inverted_list = {}
        H = {}
        for x in range(len(records)):
            candidates = []
            pp = len(records[x]) - math.ceil(threshold*len(records[x])) +1
            for i in range(pp):
                w = records[x][i]
                if w in inverted_list:
                    for j in range (len (inverted_list[w])):
                        y,py = inverted_list[w][j]
                        if len (records[y]) >=  threshold * len (records[x]) and len (records[y]) <=  len (records[x])/threshold :
                            t = math.ceil (threshold * (len (records[x]) + len (records[y])) / (1 + threshold))  # overlap threshhold
                            upbound =  min(len(records[x])-i,len(records[y])-py) + 1
                            if t <= upbound:
                                a = max(x,y)
                                b = min(x,y)
                                if (a,b) not in H:
                                    H[(a,b)] = 1
                                    candidates.append([x,y,i,py,t])
                    pi = len(records[x]) - math.ceil (2 * threshold * len(records[x]) / (1 + threshold)) + 1
                    if i < pi:
                        inverted_list[w].append ([x, i])
                else:
                    inverted_list[w] = [[x, i]]
            for e in candidates:
                similarity, olap = verify (records[e[0]], records[e[1]], e[4], 0, e[2], e[3])
                if similarity:
                    result.append ((e[0], e[1], olap))
        print('result size: ', len(result))
        print(result)
    
    if __name__ == '__main__':
        path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number.txt'
        path2 = r'E:\rochover\PycharmProjects\pengxiang_hua\data_lake\test\test_number.txt'
    
        start = time.time()
        with open (path, 'r', encoding='utf8') as f:
            r = f.readlines()
        records = statistics(r)
        end = time.time ()
        elapsed = asMinutes (end - start)
        print ('prepare time:    ', elapsed)
    
        print ('->' * 10, 'starting', '->' * 10)
        ppjoin(records,0.8)
        print ('<-' * 10, 'end', '<-'* 10)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
