---
title: pengxiang_hua_utlities_random_select
date: 2020-05-07
---
Example Python program pengxiang_hua_utlities_random_select.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import  math
* import numpy as np
* import  struct
* from utlities.time_evaluate import *

## Methods

* def random_select(in_path,out_path):
* def sampling_without_replacement(origin,size):
* def random_select_number(in_path,out_path):
* def records2bytes(records):
* def parse4bytes(filepath):

## Code

Python example

    import  math
    import numpy as np
    import  struct
    from utlities.time_evaluate import *
    
    def random_select(in_path,out_path):
        result = []
        with open (in_path,encoding='utf8') as fin :
            temp = fin.readlines()
            index = list(range(len(temp)))
            size = math.floor(len(temp)*0.2)
    
            sample = sampling_without_replacement(index,size)
            for i in sample:
                result.append (temp[i])
            with open (out_path+'2.txt', mode='w', encoding='utf8') as f:
                f.writelines (result)
    
            r4 = list (set (index).difference (set (sample)))
            sample4 =sampling_without_replacement(r4,size)
            for i in sample4:
                result.append (temp[i])
            sample = np.concatenate((sample,sample4))
            with open (out_path+'4.txt', mode='w', encoding='utf8') as f:
                f.writelines (result)
    
            r6 = list (set (index).difference (set (sample)))
            sample6 = sampling_without_replacement (r6, size)
            for i in sample6:
                result.append (temp[i])
            sample = np.concatenate((sample,sample6))
            with open (out_path + '6.txt', mode='w', encoding='utf8') as f:
                f.writelines (result)
    
            r8 = list (set (index).difference (set (sample)))
            sample8 = sampling_without_replacement (r8, size)
            for i in sample8:
                result.append (temp[i])
            with open (out_path + '8.txt', mode='w', encoding='utf8') as f:
                f.writelines (result)
    
    def sampling_without_replacement(origin,size):
        r = np.random.choice(origin,size,replace=False)
        return r
    
    @timer
    def random_select_number(in_path,out_path):
        g = parse4bytes(in_path)
        records = []
        while g :
            record = []
            id = next(g)
            if id == -1:
                break
            size = next(g)
            record.extend([id,size])
            for _ in range(size):
                record.append(next(g))
            records.append(record)
    
        print('reading finish.')
    
    
        result = []
    
        index = list (range (len (records)))
        size = math.floor (len (records) * 0.2)
    
        sample = sampling_without_replacement (index, size)
        print ('write starts...')
        with open (out_path + '2.txt.bin', mode='ab') as f:
            count = 0
            for i in sample:
                result.append (records[i])
                count +=1
                if count%1000 == 0:
                    s = records2bytes(result)
                    f.write(s)
                    result = []
                    count = 0
            s = records2bytes (result)
            f.write (s)
    
    
    
        r4 = list (set (index).difference (set (sample)))
        sample4 = sampling_without_replacement (r4, size)
        sample = np.concatenate ((sample, sample4))
        with open (out_path + '4.txt.bin', mode='ab') as f:
            count = 0
            result = []
            for i in sample:
                result.append (records[i])
                count +=1
                if count%1000 == 0:
                    s = records2bytes(result)
                    f.write(s)
                    result = []
                    count = 0
            s = records2bytes (result)
            f.write (s)
    
        r6 = list (set (index).difference (set (sample)))
        sample6 = sampling_without_replacement (r6, size)
        sample = np.concatenate ((sample, sample6))
        with open (out_path + '6.txt.bin', mode='ab') as f:
            count = 0
            result = []
            for i in sample:
                result.append (records[i])
                count += 1
                if count % 1000 == 0:
                    s = records2bytes (result)
                    f.write (s)
                    result = []
                    count = 0
            s = records2bytes (result)
            f.write (s)
    
        r8 = list (set (index).difference (set (sample)))
        sample8 = sampling_without_replacement (r8, size)
        sample = np.concatenate ((sample, sample8))
        with open (out_path + '8.txt.bin', mode='ab') as f:
            count = 0
            result = []
            for i in sample:
                result.append (records[i])
                count += 1
                if count % 1000 == 0:
                    s = records2bytes (result)
                    f.write (s)
                    result = []
                    count = 0
            s = records2bytes (result)
            f.write (s)
    
    def records2bytes(records):
        result = b''
        for record in records:
            s = struct.pack ('@{}I'.format (len(record)), *record)
            result += s
        return result
    
    def parse4bytes(filepath):
        chunk_size = 4
        with open (filepath, mode='rb') as fin:
            while True:
                chunk = fin.read (chunk_size)
                if chunk:
                    e = struct.unpack ('<I', chunk)[0]
                    yield e
                else:
                    yield -1
    
    
    if __name__ == '__main__':
        in_path = r'E:\rochover\dataset\set similarity\numbers\livej.txt.bin'
        out_path = r'E:\rochover\dataset\set similarity\numbers\livej-0.'
        # random_select(in_path,out_path)
        random_select_number(in_path,out_path)
        # parseFile(in_path)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
