---
title: ec_datetime_arange
date: 2020-05-07
---
Example Python program ec_datetime_arange.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import pandas as pd

## Code

Python example

    # taken from Coursera.org
    
    %matplotlib notebook
    import numpy as np
    import matplotlib.pyplot as plt
    import pandas as pd
    
    linear_data = np.array([1,2,3,4,5,6,7,8])
    exponential_data = linear_data**2
    
    plt.figure()
    
    observation_dates = np.arange('2017-03-01', '2017-03-09', dtype='datetime64[D]')
    # the line above returns a numpy datetime array. it cannot be directly plotted into the matplotlib, since matplotlib
    #    expects standard python datetime format. 
    # thus, we need to convert the datetime to the standard format, using help from pandas --> pd.to_datetime. 
    
    observation_dates2 = map(pd.to_datetime, observation_dates)
    # the line above returns a list in a map object format. This map object consists of iterators, not the real list 
    #    (iterables). 
    # iterator is just like a pointer. it is just pointing to the record and we still need to figure out to what record
    #    the iterator points to. 
    # thus, we need to convert the map object (iterator) to a list format. 
    
    observation_dates3 = list(observation_dates2)
    # the line above solves the problem regarding operators. 
    # but this is not a memory-efficient way to handle the data.
    
    plt.plot(observation_dates3, linear_data, '-o',  observation_dates3, exponential_data, '-o')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
