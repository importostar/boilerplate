---
title: nfl_bucketize
date: 2020-05-07
---
Example Python program nfl_bucketize.py

## Modules

* import numpy as np
* import pandas as pd

## Methods

* def bucketize(df):

## Code

Python example

    import numpy as np
    import pandas as pd
    
    five38 = winConf[winConf.FTE.notnull()][['win_prob', 'FTE', 'FTE_cnt']]
    print five38.head()
    
    #    win_prob       FTE  FTE_cnt
    # 1      0.50  0.000000        4
    # 2      0.51  0.666667        6
    # 3      0.52  0.555556        9
    # 4      0.53  0.625000        8
    # 5      0.54  0.400000       10
    
    
    buckets = np.arange(.5,1.05,.1)
    
    def bucketize(df):
        conf_list = []
        win_list = []
        cnt_list = []
        for i in range(len(buckets)-1):
            buck_min, buck_max = buckets[i], buckets[i+1]
            cnt_games = np.sum(df[(df.iloc[:,0]>=buck_min) & (df.iloc[:,0]<buck_max)].iloc[:,2])
            per_conf = np.round(np.sum(df[(df.iloc[:,0]>=buck_min) & (df.iloc[:,0]<buck_max)].iloc[:,0] \
                           * df[(df.iloc[:,0]>=buck_min) & (df.iloc[:,0]<buck_max)].iloc[:,2])/ cnt_games, 2)
            per_win = np.round(np.sum(df[(df.iloc[:,0]>=buck_min) & (df.iloc[:,0]<buck_max)].iloc[:,1] \
                           * df[(df.iloc[:,0]>=buck_min) & (df.iloc[:,0]<buck_max)].iloc[:,2])/ cnt_games, 2)
            conf_list.append(per_conf)
            win_list.append(per_win)
            cnt_list.append(cnt_games)
        return (conf_list, win_list, cnt_list)
        
    bucketize(five38)
    
    # ([0.55000000000000004,
    #   0.65000000000000002,
    #   0.73999999999999999,
    #   0.81999999999999995,
    #   0.90000000000000002],
    #  [0.54000000000000004,
    #   0.57999999999999996,
    #   0.70999999999999996,
    #   0.84999999999999998,
    #   1.0],
    #  [85L, 60L, 42L, 20L, 1L])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
