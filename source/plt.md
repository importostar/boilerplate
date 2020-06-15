---
title: plt
date: 2020-05-07
---
Example Python program plt.py

## Modules

* import matplotlib.pyplot as plt

## Code

Python example

    import matplotlib.pyplot as plt
    
    #创建一个Figure,figuresize：大小，num=编号
    fig = plt.figure(figuresize=[8,16],num=2)
    #得到当前figure的引用，get current figure
    fig1= plt.gcf()
    fig == fig1
    
    #分成m=3,n=2的子图，在第i=1的位置创建子图
    ax1 = plt.add_subplot(3,2,1)
    ax2 = plt.add_subplot(3,2,2)
    ax1.plot(1,2)
    
    #可以一次创建所有子图,ax是所有子图组成的list
    fig,ax = plt.subplots(nrows=3,ncols=2)
    
    x = np.linspace(0, 2*np.pi, 400)
    y = np.sin(x**2)
    # Just a figure and one subplot
    f, ax = plt.subplots()
    ax.plot(x, y)
    ax.set_title('Simple plot')
    
    # Two subplots, unpack the output array immediately
    f, (ax1, ax2) = plt.subplots(1, 2, sharey=True)
    ax1.plot(x, y)
    ax1.set_title('Sharing Y axis')
    ax2.scatter(x, y)
    # Four polar axes
    plt.subplots(2, 2, subplot_kw=dict(polar=True))
    # Share a X axis with each column of subplots
    plt.subplots(2, 2, sharex='col')
    # Share a Y axis with each row of subplots
    plt.subplots(2, 2, sharey='row')
    # Share a X and Y axis with all subplots
    plt.subplots(2, 2, sharex='all', sharey='all')
    # same as
    plt.subplots(2, 2, sharex=True, sharey=True)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
