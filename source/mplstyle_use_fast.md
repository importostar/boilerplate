---
title: mplstyle_use_fast
date: 2020-05-07
---
Example Python program mplstyle_use_fast.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.style as mplstyle
* import matplotlib

## Code

Python example

    %matplotlib
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.style as mplstyle
    plt.rcParams['font.size']=14
    #Using matplotlib backend: Qt5Agg
    
    #make_data
    data_10k = np.random.rand(10000)
    data_100k = np.random.rand(100000)
    data_1000k = np.random.rand(1000000)
    
    
    %%timeit
    fig,ax = plt.subplots()
    ax.plot(data_10k)
    plt.show()
    plt.close()
    #154 ms ± 27.1 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    
    %%timeit
    fig,ax = plt.subplots()
    ax.plot(data_100k)
    plt.show()
    plt.close()
    #217 ms ± 48.9 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    
    %%timeit
    fig,ax = plt.subplots()
    ax.plot(data_1000k)
    plt.show()
    plt.close()
    #379 ms ± 59.7 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    
    
    mplstyle.use('fast')
    
    %%timeit
    fig,ax = plt.subplots()
    ax.plot(data_10k)
    plt.show()
    plt.close()
    #156 ms ± 22.2 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    
    %%timeit
    fig,ax = plt.subplots()
    ax.plot(data_100k)
    plt.show()
    plt.close()
    #182 ms ± 13.6 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    
    %%timeit
    fig,ax = plt.subplots()
    ax.plot(data_1000k)
    plt.show()
    plt.close()
    #265 ms ± 33.1 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    
    
    normal=np.array([154,217,379])
    normal_err = np.array([27.1,48.9 ,59.7])
    fast=np.array([156,182,265])
    fast_err = np.array([22.2,13.6,33.1])
    
    fig,ax = plt.subplots()
    x=np.arange(3)-.1
    xx=np.arange(3)+.1
    ax.bar(x,normal,width=.2,color='C2',yerr=normal_err,label="normal")
    ax.bar(xx,fast,width=.2,color='C6',yerr=fast_err,label='fast')
    label=['10k','100k','1000k']
    ax.set_xticks([0,1,2])
    ax.set_xticklabels(label)
    ax.set_xlabel('Amount of data')
    ax.set_ylabel('Time / ms')
    plt.legend()
    plt.savefig('fast_style.png',dpi=120)
    plt.show()
     
      
    import matplotlib
    print(matplotlib.__version__)
    #3.2.0
    
    print(np.__version__)
    #1.18.1

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
