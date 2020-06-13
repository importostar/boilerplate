---
title: pengxiang_hua_data_lake_similarity_filter_verificate_top_k_similarity
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_top_k_similarity.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* from utlities.time_evaluate import *
* import time
* from utlities.heap import HeapPriorityQueue
* from utlities.statistics import *

## Classes

* class Top_k():

## Methods

* def __init__(self,R,k):
* def top_k_similarity(self):
* def find_second_common_pos(self,x,y,e):
* def similarity_upper_bound_access(self,spx,spy):
* def similarity_upper_bound_index(self,x,px):
* def similarity_upper_bound_probe(self,x,px):
* def calc_similarity(self,x,y):
* def initializeEvents(self):
* def initializeTempResults(self):
* def calc_similarity(r,s):

## Code

Python example

    import numpy as np
    from utlities.time_evaluate import *
    import time
    from utlities.heap import HeapPriorityQueue
    from utlities.statistics import *
    
    class Top_k():
        def __init__(self,R,k):
            self.H = {}
            self.E = HeapPriorityQueue() #根据每个元素第三项值递增序列  E.sort(key=lambda x:x[2])
            self.T = HeapPriorityQueue() #Store any k pairs as temp results in T 根据每个元素第三项值递增序列  T.sort(key=lambda x:x[2])
            self.R = R
            self.k = k
    
        def top_k_similarity(self):
            #Input: R is a collection of records; each record has been
            #       canonicalized by a global ordering O
            #Output: Top-k pairs of records x, y ranked by their
            #        similarity value
            self.initializeEvents ()
            self.initializeTempResults()
            I = {}
            flag = False
            while(not self.E.is_empty()):
                x,px,tub = self.E.remove_min()
                tub = -tub
                sk = self.T.min()[2]
                if tub <= sk:
                    break
                w = self.R[x][px]
    
                if w in I:
                    for j in range(len(I[w])):
                        y,py = I[w][j]
                        a = 1 - px/len(self.R[x])
                        b = 1 - py/len (self.R[y])
                        if self.similarity_upper_bound_access(a,b) < sk:
                            I[w] = I[w][0:j]
                            break
                        if len(self.R[x])*sk <= len(self.R[y]) <= len(self.R[x])/sk:
                            a = max (x, y)
                            b = min (x, y)
                            if (a,b) not in self.H :
                                self.H[(a,b)] = 0
                                sim = self.calc_similarity (a, b)
                                if sim > sk:
                                    self.T.add([a,b,sim])
                                    self.T.remove_min()
                                sk = self.T.min()[2]
                    # I[w].append ([x, px])
                    if flag == False:
                        si = self.similarity_upper_bound_index (x, px)
                        if si >= sk:
                            I[w].append ([x, px])
                        else:
                            flag = True
                else:
                    I[w] = [[x,px]]
                spx = self.similarity_upper_bound_probe(x,px+1)
                if spx > sk:
                    self.E.add([x,px+1,-spx])
            print ('events_size；    ', len (self.E))
            result = []
            while not self.T.is_empty():
                item = self.T.remove_min()
                print(item)
                result.append(item)
            path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number_topk_0.8.txt'
            with open (path, 'w', encoding='utf8') as f:
                for item in result:
                    f.writelines(str(item)+'\n')
    
        def find_second_common_pos(self,x,y,e):
            posx = self.R[x].index(e)
            posy = self.R[y].index (e)
            while posx < len(self.R[x])-1:
                posx += 1
                if self.R[x][posx] in self.R[y]:
                    posy = self.R[y].index (self.R[x][posx])
                    break
            return posx,posy
    
        def similarity_upper_bound_access(self,spx,spy):
            return spx*spy/(spx+spy-spx*spy)
    
        def similarity_upper_bound_index(self,x,px):
            return  (len (self.R[x]) - px )/(len (self.R[x]) + px )
    
        def similarity_upper_bound_probe(self,x,px):
            return 1 - px/len(self.R[x])
    
        def calc_similarity(self,x,y):
            s = set (self.R[x])
            r = set (self.R[y])
            result = float (len (s & r) / len (s | r))
            return result
    
        def initializeEvents(self):
            for i in range(len(self.R)):
                self.E.add([i,0,-1.0])
    
        def initializeTempResults(self):
            length  = len(self.R)
            while len(self.T) < self.k:
                t1,t2 = np.random.choice (list (range (length)), 2,replace=False)
                a = max (t1, t2)
                b = min (t1, t2)
                if (a,b) not in self.H:
                    self.H[(a, b)] = 0
                    sim = self.calc_similarity (a, b)
                    if sim == 0:
                        sim = 0.0000000001
                        # continue
                    self.T.add ([a, b, sim])
    
    def calc_similarity(r,s):
        s = set (s)
        r = set (r)
        rs = len (s & r)
        similarity = float (rs) / (len (r) + len (s) - rs)
        return similarity
    
    if __name__ == '__main__':
        path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number.txt'
        path2 = r'E:\rochover\PycharmProjects\pengxiang_hua\data_lake\test\test_number.txt'
    
        start = time.time ()
        with open (path, 'r', encoding='utf8') as f:
            r = f.readlines ()
        records = statistics(r)
        end = time.time ()
        elapsed = asMinutes (end - start)
        print ('prepare time:    ', elapsed)
    
    
        print ('->' * 10, 'starting', '->' * 10)
        start = time.time ()
        topk = Top_k(records,1263)
        topk.top_k_similarity()
    
        end = time.time ()
        print ('<-' * 10, 'end', '<-' * 10)
        elapsed = asMinutes (end - start)
        print ('elapsed :    ', elapsed)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
