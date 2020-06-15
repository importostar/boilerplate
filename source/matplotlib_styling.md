---
title: matplotlib_styling
date: 2020-05-07
---
Example Python program matplotlib_styling.py

## Modules

* from matplotlib import pyplot as plt

## Methods

* def set_styling(style='fivethirtyeight'):

## Code

Python example

    from matplotlib import pyplot as plt
    """If used in Jupyter notebook, this can be embeded by adding cell:
    
    %%bash
    if [ ! -e matplotlib_styling.py ]; then
        wget https://gist.githubusercontent.com/izikeros/457a99d950310da8166050a13f4043cb/raw/4334d77bdaad867003926e7cf87ffbec7131528d/matplotlib_styling.py
    fi
    """
    
    def set_styling(style='fivethirtyeight'):
        """
        Set styling details for matplotlib.
    
        References:
            http://www.futurile.net/2016/02/27/matplotlib-beautiful-plots-with-style/
            https://seaborn.pydata.org/tutorial/aesthetics.html
    
        """
        # Set the style globally
        # Alternatives include bmh, fivethirtyeight, ggplot,
        # dark_background, seaborn-deep, seaborn-pastel, seaborn-white, xkcd etc
        #
        # Big list of styles:
        #   plt.style.available
        plt.style.use(style)
    
        fs_small = 14  # 8
        fs_medium = 16  # 10
        fs_big = 18  # 12
        plt.rcParams['font.family'] = 'sans-serif' #'serif'
        plt.rcParams['font.serif'] = 'Ubuntu'
        plt.rcParams['font.monospace'] = 'Ubuntu Mono'
        plt.rcParams['font.size'] = fs_medium
        plt.rcParams['axes.labelsize'] = fs_medium
        plt.rcParams['axes.labelweight'] = 'bold'
        plt.rcParams['axes.titlesize'] = fs_medium
        plt.rcParams['xtick.labelsize'] = fs_small
        plt.rcParams['ytick.labelsize'] = fs_small
        plt.rcParams['legend.fontsize'] = fs_medium
        plt.rcParams['figure.titlesize'] = fs_big
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
