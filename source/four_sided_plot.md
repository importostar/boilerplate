---
title: four_sided_plot
date: 2020-05-07
---
Example Python program four_sided_plot.py

## Modules

* import numpy as np
* from matplotlib import pyplot as plt

## Code

Python example

    import numpy as np
    from matplotlib import pyplot as plt
    
    # Generate fake data
    np.random.seed(123)
    wavelen = np.arange(500, 1000, 8)
    fluxden = -wavelen**2/1000 + 2*wavelen + np.random.normal(loc=0, scale=5, size=len(wavelen))
    fluxerr = np.sqrt(fluxden)
    
    # Default plot with errorbars
    fig, ax = plt.subplots(nrows=1, ncols=1)
    ax.errorbar(wavelen, fluxden, yerr=fluxerr, marker='.', ls=':', capsize=3)
    
    ################################################################################
    # Simple answer
    ################################################################################
    ax.tick_params(axis='both',                    # Which axis ('x', 'y', 'both')
                   direction='in',                 # Which direction ('in', 'out', 'inout')
                   top=True, bottom=True,          # Whether to show ticks on top, bot, left, right
                   left=True, right=True,
                   labeltop=True, labelbottom=True, # Whether to show labels on top, etc
                   labelleft=True, labelright=True)
    # REF: https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.tick_params.html
    
    plt.show()
    
    
    ################################################################################
    # A bit complicated answer
    ################################################################################
    # Default plot with errorbars
    fig, ax = plt.subplots(nrows=1, ncols=1)
    ax.errorbar(wavelen, fluxden, yerr=fluxerr, marker='.', ls=':', capsize=3)
    
    # Make ticks to the inside at all 4 axes
    alltick = dict(top=True, bottom=True, left=True, right=True,                     # Whether to show ticks
                   labeltop=True, labelbottom=True, labelleft=True, labelright=True) # Whether to show labels
    
    ax.tick_params(axis='both',    # Which axis ('x', 'y', 'both')
                   direction='in', # Which direction ('in', 'out', 'inout')
                   length=5,       # Tick length
                   width=2,        # Tick width
                   color='b',      # Tick color ('k' for black, etc)
                   pad=10,         # Tick & label distance
                   **alltick)
    # REF: https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.tick_params.html
    # INFO: ``**alltick`` is identical to directly put ``top=Ture, bottom=True, .....`` in this case.
    
    # Put grid
    ax.grid(ls=':')
    
    # x-axis: "wavelength" with blue color
    ax.set_xlabel("Wavelength [nm]", color='b')
    ax.tick_params(axis='x', colors='b')
    
    # y-axis: "intensity" with green color
    ax.set_ylabel("Intensity [arbitrary]", color='g')
    ax.tick_params(axis='y', colors='g')
    
    # Put title
    ax.set_title(r"LaTeX Style title: $F=ma$", y=1.1)
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
