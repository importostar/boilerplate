---
title: boxplots
date: 2020-05-07
---
Example Python program boxplots.py

## Modules

* import numpy as np

## Methods

* def make_boxplot(ax, data, title):

## Code

Python example

    import numpy as np
    figsize = (10, 4) # set the fgsize for both the box plots and histograms
    # make boxplots
    
    # notch shape box plot
    
    def make_boxplot(ax, data, title):
        labels = [d.name for d in data]
        ax.boxplot(data,
                    notch=True,  # notch shape
                    vert=True,   # vertical box aligmnent
                    labels=labels,
                    patch_artist=False,
                    showbox=True,
                    showfliers=False)   # fill with color
        ax.set_title(title)
        
        # jittered data points, see <https://stackoverflow.com/questions/23519135>
        # seaborn does this better
        for i, d in enumerate(data):
            y = data[i]
            x = np.random.normal(i+1, 0.02, len(y))
            ax.plot(x, y, 'r.', alpha=0.6)
        
    fig, ax = plt.subplots(ncols=3, figsize=figsize)
    
    make_boxplot(ax[0], (df_deduped["asym_m"], df_deduped["asym_a"]), "asym")
    make_boxplot(ax[1], (df_deduped["plates_m"], df_deduped["plates_a"]), "plates per m")
    make_boxplot(ax[2], (df_deduped["hetp_m"], df_deduped["hetp_a"]), "hetp")
    plt.tight_layout()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
