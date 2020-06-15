---
title: pengxiang_hua_data_lake_similarity_prepare_prepare_word2number
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_prepare_prepare_word2number.py

## Modules

* import re
* from utlities.time_evaluate import *

## Methods

* def build_word2number(in_path,out_path,word2index_path):
* def build_word2count(s):
* def build_word2index(s):

## Code

Python example

    import re
    from utlities.time_evaluate import *
    
    word2count = {}
    word2index = {}
    
    @timer
    def build_word2number(in_path,out_path,word2index_path):
    
        with open(in_path,mode='r',encoding='utf8') as f:
            records = f.readlines()
    
        for record in records:
            rstr = r"[\=\(\)\,\/\\\:\*\?\"\<\>\|\' ']"
            s = re.sub (rstr, ' ', record).lower ().rstrip ('.').strip ()
            s = list (set (s.split ()))
            build_word2count (s)
    
        words = list (word2count.keys ())
        words.sort (key=lambda x: word2count[x])
        size = len (words)
        global word2index
        for i in range (size):
            word2index[words[i]] = i
    
        number_records = []
        for record in records:
            rstr = r"[\=\(\)\,\/\\\:\*\?\"\<\>\|\' ']"
            s = re.sub (rstr, ' ', record).lower ().rstrip ('.').strip ()
            s = list (set (s.split ()))
            temp = build_word2index(s)
            if len(temp)> 0 :
                number_records.append(' '.join('%s' %id for id in temp).strip()+'\n')
    
        number_records = list(set(number_records))#去重
        number_records.sort(key=lambda x:len(x))#排序
    
        with open(out_path,mode='w',encoding='utf8') as f:
            f.writelines(number_records)
        with open(word2index_path,mode='w',encoding='utf8') as f:
            f.writelines(str(word2index))
    
    
    def build_word2count(s):
        global  word2count
        for word in s:
            if word not in word2count:
                word2count[word] = 1
            else:
                word2count[word] += 1
    
    def build_word2index(s):
        global word2index
        temp = []
        for word in s:
            temp.append(word2index[word])
        temp = list(set(temp))
        temp.sort()
    
        return temp
    
    if __name__ == '__main__':
        in_path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut-0.2.txt'
        out_path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut-0.2_number.txt'
        word2index_path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut-0.2_word2index.txt'
        build_word2number(in_path,out_path,word2index_path)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
