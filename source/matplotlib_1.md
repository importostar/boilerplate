---
title: matplotlib_1
date: 2020-05-07
---
Example Python program matplotlib_1.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np

## Methods

* def f(x, y):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import numpy as np
    plt.style.use('Solarize_Light2')
    plt.style.use('fivethirtyeight')
    plt.style.use('classic')
    plt.style.use('tableau-colorblind10')
    plt.style.use('ggplot')
    
    fig, axes = plt.subplots(ncols=3, nrows=1,figsize=(12,4))
    ax = axes.ravel()
    
    # scatter plot (Note: `plt.scatter` doesn't use default colors)
    x, y = np.random.normal(size=(2, 100))
    ax[0].plot(x, y, 'o')
    # histogram
    data_1 = np.random.randn(1000)
    data_2 = np.random.randn(1000)
    ax[1].hist(data_1,alpha=0.5)
    ax[1].hist(data_2,alpha=0.5)
    
    # contour
    def f(x, y):
        return np.cos(x+y) ** 5 + np.cos(4 + y * x) * np.cos(-x)
    x = np.linspace(0, 5, 100)
    y = np.linspace(0, 5, 100)
    X, Y = np.meshgrid(x, y)
    Z = f(X, Y)
    ax[2].contour(X, Y, Z)
    ax[2].axis('scaled')
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
