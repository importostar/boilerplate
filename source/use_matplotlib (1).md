---
title: use_matplotlib (1)
date: 2020-05-07
---
Example Python program use_matplotlib (1).py

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt

## Code

Python example

    import matplotlib as mpl
    import matplotlib.pyplot as plt
    
    #####################################
    # BAISC
    #####################################
    
    # Set style e.g.'seaborn-whitegrid', 'ggplot'
    plt.style.use('classic')
    
    # Choose the option to embed graphics in notebook
    # Use notebook for interactive plots and inline for static plots
    %matplotlib inline
    
    # 1. MATLAP style interface
    # Create a figure => create the panel => plot on the current panel
    plt.figure()
    
    plt.subplot(2, 1, 1) # (rows, columns, panel number)
    plt.plot(x, np.sin(x))
    
    plt.subplot(2, 1, 2)
    plt.plot(x, np.cos(x))
    plt.show()
    
    # directly use plt.plot() such that figure and axes will be created on the background themselves
    plt.plot(x, np.sin(x), label='sin(x)')
    plt.plot(x, np.cos(x), label='cos(x)')
    plt.legend()
    
    # adjust limits with plt
    plt.xlim(-1, 11)
    plt.ylim(-1.5, 1.5)
    # or use axis() with a single call
    # e.g. plt.axis([-1, 11, -1.5, 1.5]) plt.axis('tight') plt.axis('equal')
    
    # title and label
    plt.title("A Sine and Cosine Curve")
    plt.xlabel("x")
    plt.ylabel("y");
    
    plt.show()
    
    
    # 2. Object-oriented interface
    # Create a grid of plots and get an array of Axes objects => plot() on the selected axes
    fig, ax = plt.subplots(2)
    
    ax[0].plot(x, np.sin(x))
    ax[1].plot(x, np.cos(x))
    
    
    # Create a figure and axes => plot on the axes
    fig = plt.figure()
    ax = plt.axes()
    # above lines are equal to fig, ax = subplots()
    
    x = np.linspace(0, 10, 1000)
    ax.plot(x, np.sin(x))
    
    # adjust ax
    ax.set(xlim=(0, 10), ylim=(-2, 2),
           xlabel='x', ylabel='sin(x)',
           title='A Simple Plot')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
