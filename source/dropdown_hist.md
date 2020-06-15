---
title: dropdown_hist
date: 2020-05-07
---
Example Python program dropdown_hist.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from ipywidgets import interact,Dropdown
* import seaborn as sns
* import ipywidgets
* import matplotlib

## Methods

* def f(dd):
* def f(dd):

## Code

Python example

    %matplotlib widget
    import numpy as np
    import matplotlib.pyplot as plt
    from ipywidgets import interact,Dropdown
    import seaborn as sns
    sns.set(style="ticks")
    
    #make data
    d_list=[]
    for i in np.logspace(3,5,3).astype(int):
        d = np.random.normal(0,1,i)
        d_list.append(d)
    d_hist_list=[]
    d_bins_list=[]
    
    for i in range(3):
        h,b = np.histogram(d_list[i], bins=100)
        d_hist_list.append(h)
        d_bins_list.append(b)
        
    fig, ax = plt.subplots(figsize=(6,4))
    dd = Dropdown(
        options=[('data1', 0), ('data2', 1), ('data3', 2)],
        value=0,
        description='Select data:')
    @interact(dd=dd)
    def f(dd):    
        ax.cla()
        width=d_bins_list[dd][1]-d_bins_list[dd][0]
        ax.bar(d_bins_list[dd][1:],d_hist_list[dd],width=width,color='C2')
    
    #seaborn 
    fig= plt.figure(figsize=(6,4))
    dd = Dropdown(
        options=[('data1', 0), ('data2', 1), ('data3', 2)],
        value=2,
        description='Select data:')
    axx=[]
    @interact(dd=dd)
    def f(dd):    
        if len(axx)>0:
            axx.pop().remove()
        hist =sns.distplot(d_list[dd],bins=50,kde=False)
        axx.append(hist)
        
    #version
    import ipywidgets
    print(ipywidgets.__version__)
    #7.5.1
    import matplotlib
    print(matplotlib.__version__)
    #3.2.0
    print(np.__version__)
    #1.18.1
    print(sns.__version__)
    #0.10.0
     

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
