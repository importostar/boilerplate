---
title: pengxiang_hua_data_lake_similarity_filter_verificate_all_pairs
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_all_pairs.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from data_lake.similarity.filter_verificate.verify import verify
* from utlities.time_evaluate import *
* from utlities.statistics import *

## Methods

* def all_pairs(records,jaccard_similarity_threshold):
* def calc_similarity(r,s):

## Code

Python example

    from data_lake.similarity.filter_verificate.verify import verify
    from utlities.time_evaluate import *
    from utlities.statistics import *
    @timer
    def all_pairs(records,jaccard_similarity_threshold):
        '''
         WWW'07-Scaling Up All Pairs Similarity Search
        :param records:
        :param jaccard_similarity_threshold:
        :return:
        '''
        result = []
        inverted_list = {}
        H = {}
        for x in range(len(records)):
            candidates = []
            record = records[x]
            p = len(record) - math.ceil(jaccard_similarity_threshold *len(record)) +1
            for px in range (p):
                w = record[px]
                if w in inverted_list:
                    for j in range (len (inverted_list[w])):
                        y,py = inverted_list[w][j]
                        if len (records[y]) >= jaccard_similarity_threshold * len (record) and len (records[y]) <= len (record)/jaccard_similarity_threshold :
                            a = max(x,y)
                            b = min(x,y)
                            if (a,b) not in H:
                                H[(a,b)] = 1
                                candidates.append([x,y,px,py])
                    pi = len (record) - math.ceil (
                        2 * jaccard_similarity_threshold * len (record) / (1 + jaccard_similarity_threshold)) + 1
                    if px < pi:
                        inverted_list[w].append([x,px])
                else:
                    inverted_list[w] = [[x,px]]
            for e in candidates:
                t = math.ceil (jaccard_similarity_threshold *(len (records[e[0]])+len (records[e[1]])) /(1+jaccard_similarity_threshold))  # overlap threshhold
                similarity,olap = verify (records[e[0]],records[e[1]],t,0,e[2],e[3])
                if similarity:
                    result.append ((e[0],e[1],olap))
        print('result size: ',len(result))
        print (result)
        path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number_all_pairs_0.8.txt'
        with open(path,'w',encoding='utf8') as f:
            for item in result:
                f.writelines(str(item)+'\n')
    
    def calc_similarity(r,s):
        s = set (s)
        r = set (r)
        rs = len (s & r)
        similarity = float (rs) / (len (r) + len (s) - rs)
        return similarity
    if __name__ == '__main__':
        path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number.txt'
        path2 = r'E:\rochover\PycharmProjects\pengxiang_hua\data_lake\test\test_number.txt'
    
        start = time.time()
        with open (path2, 'r', encoding='utf8') as f:
            r = f.readlines()
        records = statistics(r)
        end = time.time ()
        elapsed = asMinutes (end - start)
        print ('prepare time:    ', elapsed)
    
        print ('->' * 10, 'starting', '->' * 10)
        all_pairs(records,0.8)
        print ('<-' * 10, 'end', '<-'* 10)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
