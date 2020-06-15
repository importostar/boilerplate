---
title: pengxiang_hua_data_lake_similarity_filter_verificate_ppjion+
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_ppjion+.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import math
* from data_lake.similarity.filter_verificate.verify import verify
* from utlities.time_evaluate import *
* from utlities.statistics import *

## Methods

* def ppjoin_plus(records,threshold):
* def suffixfilter(x, y,hmax, d):
* def partion(s,w,l,r):
* def find_first_gt_or_eq_sk(list_t,w,start,end):

## Code

Python example

    import math
    from data_lake.similarity.filter_verificate.verify import verify
    from utlities.time_evaluate import *
    from utlities.statistics import *
    
    MAXDEPTH = 2
    
    @timer
    def ppjoin_plus(records,threshold):
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
            for px in range(pp):
                w = records[x][px]
                if w in inverted_list:
                    for j in range (len (inverted_list[w])):
                        y,py = inverted_list[w][j]
                        if len (records[y]) >=  threshold * len (records[x]) and len (records[y]) <=  len (records[x])/threshold :
                            t = math.ceil (threshold * (len (records[x]) + len (records[y])) / (1 + threshold))  # overlap threshhold
                            upbound =  min(len(records[x])-px,len(records[y])-py) + 1
                            if t <= upbound:
                                a = max(x,y)
                                b = min(x,y)
                                if (a,b) not in H:
                                    hmax = len(records[x])+len(records[y]) - 2 * t - (px+py-2)
                                    h = suffixfilter(records[x][px+1:],records[y][py+1:],hmax,1)
                                    H[(a, b)] = 1
                                    if h <= hmax:
                                        candidates.append([x,y,px,py,t])
                    pi = len(records[x]) - math.ceil ( 2*threshold * len(records[x]) / (1 + threshold)) + 1
                    if px < pi:
                        inverted_list[w].append ([x, px])
                else:
                    inverted_list[w] = [[x, px]]
            for e in candidates:
                similarity, olap = verify (records[e[0]], records[e[1]], e[4], 0, e[2], e[3])
                if similarity:
                    result.append ((e[0], e[1], olap))
        print('result size: ', len(result))
        print(result)
    
    def suffixfilter(x, y,hmax, d):
        '''
        :param x:set of tokens
        :param y:set of tokens
        :param hmax:the maximum allowable hamming distance hmax between x and y
        :param d:current recursive depth d
        :return:The lower bound of hamming distance between x and y
        '''
        dif_x_y = abs(len(y) - len(x))
        if d > MAXDEPTH or len(y) == 0 or len(x) == 0:
            return dif_x_y
        mid = len(y)//2
        w = y[mid]
        yl, yr, f, dif = partion (y, w, mid, mid)
    
        o = (hmax-dif_x_y)//2
        if len(x) < len(y):
            oleft = 1
            oright = 0
        else:
            oleft = 0
            oright = 1
    
        l =  max(mid - o - dif_x_y * oleft,0)
        r =  min(mid + o + dif_x_y * oright,len(x)-1)
    
        xl,xr,f,dif = partion(x,w,l,r)
        if f == 0:
            return  hmax
        h = abs(len(xl)-len(yl)) + abs(len(xr)-len(yr)) + dif
        if h > hmax:
            return  h
        else:
            hl = suffixfilter(xl,yl,hmax-abs(len(xr)-len(yr))-dif,d+1)
            h = hl + abs(len(xr)-len(yr)) + dif
            if h <= hmax:
                hr = suffixfilter(xr,yr,hmax-hl-dif,d+1)
                return hl + hr + dif
            else:
                return  h
    
    
    
    def partion(s,w,l,r):
        '''
        :param s: set of tokens s,
        :param w: a token w
        :param l: left and right bounds of searching range
        :param r:
        :return: Two subsets  of s: sl and sr, a flag f indicating whether w
                 is in the searching range, and a flag diff indicating
                 whether the probing token w is not found in y
        '''
        if s[l] > w :
            return [[],s,0,1]
        if s[r] < w :
            return [s,[],0,1]
        #p: binary search for the position of the first token in s that
        # is no smaller than w in the global ordering within s[l . . r];
        p = find_first_gt_or_eq_sk(s,w,l,r)
        sl = s[:p]
        if s[p] == w:
            sr = s[p+1:]
            dif = 0
        else:
            sr = s[p:]
            dif = 1
        return  [sl,sr,1,dif]
    
    
    def find_first_gt_or_eq_sk(list_t,w,start,end):
    
        left = start
        right = end
        while left < right:
            mid = (right-left)//2 + left
            if w == list_t[mid]:
                while start <= mid - 1 < end and w == list_t[mid - 1]:
                    mid -= 1
                return mid
            elif w < list_t[mid]:
                right = mid - 1
            else:
                left = mid + 1
        while  right < len(list_t) and w > list_t[right]:
            right += 1
        return min(right,len(list_t)-1)
    
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
        ppjoin_plus(records,0.8)
        print ('<-' * 10, 'end', '<-'* 10)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
