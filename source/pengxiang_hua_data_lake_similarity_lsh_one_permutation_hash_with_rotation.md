---
title: pengxiang_hua_data_lake_similarity_lsh_one_permutation_hash_with_rotation
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_lsh_one_permutation_hash_with_rotation.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import random
* import math

## Methods

* def oph_rotation(matrix,query):
* def find_first_nonE(vec,index):

## Code

Python example

    import numpy as np
    import random
    import math
    
    '''
    Input:matrix,nparray,row:feature.column:record
            query,nparray
    '''
    def oph_rotation(matrix,query):
        bin_size = 2
        features_size = matrix.shape[0]
        records_size = matrix.shape[1]
        bin_number = math.ceil(features_size/bin_size)
        C = bin_size + 1
        result =np.array(['E']*bin_number*records_size).reshape(records_size,bin_number)
    
        for i in range (records_size):
            for j in range (bin_number):
                for k in range(bin_size):
                    if j * bin_size + k < features_size:
                        if matrix[j * bin_size + k][i] == 0:
                            continue
                        else:
                            result[i][j] = k
                            break
    
        for i in range (records_size):
            for j in range(bin_number):
                if result[i][j] == 'E':
                    value = find_first_nonE (result[i], j)
                    result[i][j] = int(value) + C
        print(result)
        result = result.T
        for i in range(result.shape[0]):
            for j in range(result.shape[1]):
                pass
    
    
    def find_first_nonE(vec,index):
        for i in range(index+1,len(vec)):
            if vec[i] != 'E':
                return vec[i]
        for i in range (0, index):
            if vec[i] != 'E':
                return vec[i]
    
    if __name__ == '__main__':
        matrix = [[1, 0, 1, 0],
                  [1, 0, 0, 1],
                  [0, 1, 0, 1],
                  [0, 1, 0, 1],
                  [0, 1, 0, 1],
                  [1, 0, 1, 0],
                  [1, 0, 1, 0]]
        query = [1, 1, 0, 0, 0, 1, 1]
        matrix = np.array(matrix)
        matrix = np.column_stack((matrix,query))
        oph_rotation(matrix,query)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
