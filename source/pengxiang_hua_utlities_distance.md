---
title: pengxiang_hua_utlities_distance
date: 2020-05-07
---
Example Python program pengxiang_hua_utlities_distance.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* from  utlities.time_evaluate import  timer

## Methods

* def  levenshtein_distance_base(str_a,str_b):
* def  levenshtein_distance_improve(str_a,str_b):
* def addEx2H(H,list_Ex,x):
* def find_match(r,s,i,j):

## Code

Python example

    import numpy as np
    from  utlities.time_evaluate import  timer
    
    @timer
    def  levenshtein_distance_base(str_a,str_b):
    
        dp = np.zeros((len(str_a)+1,len(str_b)+1))
        for i in range(1,len(str_a)+1):
            dp[i][0] = i
        for j in range(1,len(str_b)+1):
            dp[0][j] = j
    
        for i in range(1,len(str_a)+1):
            for j in range(1,len(str_b)+1):
                flag = 0 if str_a[i-1] == str_b[j-1] else 1
                dp[i][j] = min(dp[i-1][j]+1,dp[i][j-1]+1,dp[i-1][j-1]+flag)
    
        print('levenshtein_distance_base distance:   ',dp[len(str_a)][len(str_b)])
        print('similarity: %10.2f '%(1-dp[len(str_a)][len(str_b)]/max(len(str_a),len(str_b))))
    
    @timer
    def  levenshtein_distance_improve(str_a,str_b):
    
        a = len (str_a)
        b = len (str_b)
    
        r = '0'+str_a
        s = '0'+str_b
        H = {}
        E = {}
        E[0] = find_match(r,s,-1,-1)
        addEx2H(H,E[0],0)
        for x in range(min(a,b)):
            while len(E[x]) > 0:
                i,j = E[x].pop(0)
                if x+1 not in E:
                    E[x+1] = []
                #Substitution:
                if (i+1,j+1) not in H:
                    E[x+1].append((i+1,j+1))
                    result = find_match (r, s, i + 1, j + 1)
                    E[x + 1].extend (result)
                    addEx2H (H, E[x+1], x+1)
                    if (a, b) in H.keys ():
                        print ('levenshtein_distance_improve distance:   ', H[(a, b)])
                        print ('similarity: %10.2f ' % (1 - H[(a, b)] / max (a, b)))
                        return H[(a, b)]
                #Insertion:
                if (i+1,j) not in H:
                    E[x + 1].append ((i + 1, j))
                    result = find_match (r, s, i + 1, j)
                    E[x+1].extend (result)
                    addEx2H (H, E[x+1], x+1)
                    if (a, b) in H.keys ():
                        print ('levenshtein_distance_improve distance:   ', H[(a, b)])
                        print ('similarity: %10.2f ' % (1 - H[(a, b)] / max (a, b)))
                        return H[(a, b)]
                #Deletion:
                if (i,j+1) not in H:
                    E[x + 1].append ((i, j+1))
                    result = find_match (r, s, i, j+1)
                    E[x+1].extend (result)
                    addEx2H (H, E[x+1], x+1)
                    if (a, b) in H.keys ():
                        print ('levenshtein_distance_improve distance:   ', H[(a, b)])
                        print ('similarity: %10.2f ' % (1 - H[(a, b)] / max (a, b)))
                        return H[(a, b)]
    def addEx2H(H,list_Ex,x):
        for (i,j) in list_Ex:
            if (i,j) not in H:
                H[(i,j)] = x
    
    def find_match(r,s,i,j):
        result = []
        i = i+1
        j = j+1
        while i < len(r) and j < len(s):
            if r[i] == s[j]:
                result.append((i,j))
                i = i+1
                j = j+1
            else:
                break
        return result
    
    
    while 1:
    
        str_aa = input('str_a:   ')
        str_bb = input('str_b:   ')
    
        str_a = 'zo tamiment zd overview statedestination detailednarr 18371 mapquest null 1 nj occ 28 netscape newark addrorigin pa dpc buskhill citydestination http dcc falls opc 2 addrdestination cityorigin resultsdisplaymode clients us mqtripplus stateorigin y x com road'*100
        str_b = 'zoomerang www set have is soon as deadline thanks want marthahttp tomorrow little thank for re please to so you friendly can complete far marketing completed who it link reminder those a ets i of surveythis below survey dashboard cspxmbpet01dhc6g36khwje the com zgi'*100
    
    
        print ('->' * 35)
    
        levenshtein_distance_base(str_a,str_b)
    
        levenshtein_distance_improve(str_a,str_b)
    
        print ('-*' * 35)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
