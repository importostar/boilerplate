---
title: poi_tree
date: 2020-05-07
---
Example Python program poi_tree.py

## Modules

* import codecs
* import pandas as pd
* import pickle
* import numpy as np
* import time
* from collections import Counter, namedtuple

## Methods

* def strim_csv(filename, output, sep='\t', header=0):

## Code

Python example

    # -*- coding: utf-8 -*-
    
    import codecs
    import pandas as pd
    import pickle
    import numpy as np
    import time
    
    from collections import Counter, namedtuple
    
    poi_node = namedtuple('poi_node', 'poi_id poi_name poi_parent_name poi_level')
    poi_node_s = namedtuple('poi_node_s', 'poi_id poi_name')
    
    def strim_csv(filename, output, sep='\t', header=0):
        '''
        对csv文件进行预处理，保留items数量等于众数的行便于读取
        '''
        content_raw = []
        with codecs.open(filename , 'r', encoding='utf-8') as f:
            for line in f.readlines():
                content_raw.append(line)
    
        content_len = np.array([len(x.split(sep)) for x in content_raw])
        most_common = np.argmax(np.bincount(content_len))
        content = []
        for i,x in enumerate(content_raw):
            if content_len[i] == most_common:
                content.append(x)
        with codecs.open(output, 'w', encoding='utf-8') as f:
            f.writelines(''.join(content))
    
    ## read file
    strim_csv('poi_rela.txt', 'poi_rela.txt')
    
    poi_rela = pd.read_table('poi_rela.txt', sep='\t')
    
    #poi_rela.head()
    #poi_all = pickle.load(open('static/poi_all.pickle', 'rb'))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
