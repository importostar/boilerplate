---
title: freeze_out
date: 2020-05-07
---
Example Python program freeze_out.py

## Modules

* import matplotlib
* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.ticker import MaxNLocator
* from scipy.interpolate import spline
* from numpy.random import normal

## Methods

* def equilibrium(x):
* def freezeout(x, x_fo=500.):

## Code

Python example

    """
    WIMP miracle
    ============
    """
    
    import matplotlib
    import numpy as np
    import matplotlib.pyplot as plt
    
    from matplotlib.ticker import MaxNLocator
    from scipy.interpolate import spline
    from numpy.random import normal
    
    
    matplotlib.rc('text', usetex=False)
    plt.xkcd()
    matplotlib.rc('font', **{'size': 25})
    
    
    fig, ax = plt.subplots(figsize=(8, 8))
    
    T = np.linspace(0, 50, 10)
    
    def equilibrium(x):
        """
        """
        k = 1
        return k * x**1.5 * np.exp(-x)
     
    def freezeout(x, x_fo=500.):
        """
        """
        if x < x_fo:
          return equilibrium(x)
        else:
          return equilibrium(x_fo)
    
            
    x = np.logspace(0, 4, 100)
    eq = equilibrium(x)
    fo = map(freezeout, x)
    
    plt.loglog(x, fo, color="RoyalBlue", lw=4, label="DM abundance")
    plt.loglog(x, eq, ls="--", color="Crimson", lw=4, label="Equilibrium")
    
    plt.setp(ax, yticklabels=[], xticklabels=[])
    plt.text(3, 1E-179, "Freezes-out at correct\nabundance for\nweak interaction")
    
    plt.xlabel("1/Temperature")
    plt.ylabel("Abundance")
    ax.legend(loc='lower left')
    plt.title("WIMP miracle")
            
    plt.savefig("freeze_out.png")
        

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
