---
title: pengxiang_hua_data_lake_similarity_lsh_min_hash
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_lsh_min_hash.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import hashlib
* import multiprocessing
* import traceback
* from utlities.time_evaluate import timer

## Classes

* class MyThread(multiprocessing.Process):

## Methods

* def __init__(self,func,args=()):
* def run(self):
* def get_result(self):
* def generate_signature_vector(matrix):
* def generate_signature_matrix(input_matrix,n):
* def min_hash(inputmatrix,b,r):
* def nn_search(dataSet, query):

## Code

Python example

    import numpy as np
    import hashlib
    import multiprocessing
    import traceback
    from utlities.time_evaluate import timer
    
    
    matrix=[[1,0,1,0],
            [1,0,0,1],
            [0,1,0,1],
            [0,1,0,1],
            [0,1,0,1],
            [1,0,1,0],
            [1,0,1,0]]
    query = [1,1,0,0,0,1,1]
    
    class MyThread(multiprocessing.Process):
        def __init__(self,func,args=()):
            super().__init__()
            self.func = func
            self.args = args
    
        def run(self):
            self.result = self.func(*self.args)
    
        def get_result(self):
            try:
                return  self.result
            except Exception :
                traceback.print_exc()
                return None
    
    def generate_signature_vector(matrix):
        '''
        * generate the signature vector
    
        :param matrix: a ndarray var
        :return a signature vector: a list var
        '''
        # the row sequence set
        seq_set = [i for i in range(matrix.shape[0])]
    
        # initialize the signature vector as [-1, -1, ..., -1]
        result = [-1 for _ in range(matrix.shape[1])]
        count = 0
    
        while len(seq_set) > 0:
            rdn_seq = np.random.choice(seq_set)
            for i in range(matrix.shape[1]):
                if matrix[rdn_seq][i] != 0 and result[i] == -1:
                    result[i] = rdn_seq
                    count += 1
            if count == matrix.shape[1]:
                break
            seq_set.remove(rdn_seq)
        return result
    
    def generate_signature_matrix(input_matrix,n):
        '''
    
        :param input_matrix: ndarray
        :param n: the row number of sig matrix which we set
        :return: ndarray
        '''
        r = []
        pool = multiprocessing.Pool (processes=8)
        for i in range(n):
            result = pool.apply_async(generate_signature_vector,(input_matrix,))
            r.append(result.get())
            #result.append(generate_signature_vector(input_matrix))
        pool.close()
        pool.join()
        return np.array(r)
    
    
    def min_hash(inputmatrix,b,r):
        '''
    
        :param inputmatrix: ndarray
        :param b: number of bands
        :param r: size of band
        :return: a dictionary, key is hash value, value is column number
        '''
        result={}
        signature_matrix = generate_signature_matrix(inputmatrix,b*r)
        for i in range(b):
            # traverse the column of signature_matrix
            for colNum in range (signature_matrix.shape[1]):
                # generate the hash object, we used md5
                hashObj = hashlib.md5()
                band = str(signature_matrix[i:(i+1)*r,colNum])+str(i)
                hashObj.update(band.encode())
                # use hash value as bucket tag
                tag = hashObj.hexdigest ()
    
                # update the dictionary
                if tag not in result:
                    result[tag] = [colNum]
                elif colNum not in result[tag]:
                    result[tag].append (colNum)
        return  result
    
    def nn_search(dataSet, query):
        """
        :param dataSet: 2-dimension array
        :param query: 1-dimension array
        :return: the data columns in data set that are similarity with query
        """
    
        result = set()
        input_matrix = np.array(dataSet)
        input_matrix = np.column_stack((input_matrix,query))
        hashBucket = min_hash(input_matrix, 20, 5)
    
        queryCol = input_matrix.shape[1] - 1
    
        for key in hashBucket:
            if queryCol in hashBucket[key]:
                for i in hashBucket[key]:
                    result.add(i)
    
        result.remove(queryCol)
        return result
    
    if __name__ =='__main__':
        result=nn_search(matrix,query)
        print(result)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
