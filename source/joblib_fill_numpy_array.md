---
title: joblib_fill_numpy_array
date: 2020-05-07
---
Example Python program joblib_fill_numpy_array.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import shutil
* import os
* import numpy as np
* import tempfile
* from joblib import Parallel, delayed
* from joblib import load, dump

## Methods

* def assign_row(_output, i):

## Code

Python example

    """
    Demo based on joblib documentation to fill a Numpy array in parallel
    This only works for newer version of joblib https://github.com/joblib/joblib
    """
    
    import shutil
    import os
    import numpy as np
    
    import tempfile
    from joblib import Parallel, delayed
    from joblib import load, dump
    
    
    def assign_row(_output, i):
        print("[Worker %d] Assign for row %d is %d" % (os.getpid(), i, i))
        _output[i] = i
        # print(_output[i])
    
    if __name__ == "__main__":
        folder = tempfile.mkdtemp()
        samples_folder = os.path.join(folder, 'samples')
        assign_folder = os.path.join(folder, 'assign')
    
        try:
            assign = np.memmap(assign_folder, dtype=np.float64,
                               shape=(10, 8), mode='w+')
            print("Array with shared memory:")
            print(assign)
    
            # Fork the worker processes to perform computation concurrently
            Parallel(n_jobs=4)(delayed(assign_row)(assign, i)
                               for i in range(5))
    
            print("Array with new values:")
            print(assign)
    
        finally:
            try:
                shutil.rmtree(folder)
            except:
                print("Failed to delete: " + folder)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
