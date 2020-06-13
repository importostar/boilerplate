---
title: plot_results
date: 2020-05-07
---
Example Python program plot_results.py

## Modules

* import numpy as np
* import matplotlib
* from matplotlib import pyplot as plt
* from matplotlib.collections import PatchCollection
* from matplotlib import patches

## Code

Python example

    import numpy as np
    
    import matplotlib
    from matplotlib import pyplot as plt
    
    from matplotlib.collections import PatchCollection
    from matplotlib import patches
    
    """
    This code is meant to analyse where telomeres and centromers are most often
    found in our experiments.
    """
    
    save = True
    
    X = np.load('X.npy')
    im = np.load('im.npy')
    a = np.load('im_binned.npy')
    
    patch = []
    
    art = patches.Circle((1900, 1200), 300, ec="none")
    patch.append(art)
    
    art = patches.Circle((1200, 1200), 1000, ec="none")
    patch.append(art)
    
    font = "sans-serif"
    
    fig = plt.figure(figsize=(6, 6))
    ax = fig.add_subplot(111)
    
    ax.set_xlim((-1.2, 1.2))
    ax.set_ylim((-1.2, 1.2))
    
    # add a the nucleolus
    plt.text(0.7, 0 - 0.15, "Nucleolus", ha="center",
            family=font, size=14)
    
    nucleolus = patches.Circle((0.7, 0), 0.3, ec="none")
    nucleus = patches.Circle((0, 0), 1, ec="none")
    
    collection = PatchCollection([nucleolus, nucleus],
                                 match_original=False, linewidth=2,
                                 linestyle='--', facecolor='None')
    ax.add_collection(collection)
    ax.scatter(X[:, 0], X[:, 1], alpha=0.2)
    ax.set_axis_off()
    if save:
        fig.savefig('im1.png')
    
    fig = plt.figure(figsize=(6, 6))
    ax = fig.add_subplot(111)
    
    ax.set_xlim((0, 2400))
    ax.set_ylim((0, 2400))
    
    # add a the nucleolus
    plt.text(1900, 1200, "Nucleolus", ha="center",
            family=font, size=14)
    
    collection = PatchCollection(patch, match_original=False, linewidth=2,
                                 linestyle='--', facecolor='None')
    ax.add_collection(collection)
    ax.matshow(a)
    ax.set_axis_off()
    if save:
        fig.savefig('im2.png')
    
    
    fig = plt.figure(figsize=(6, 6))
    ax = fig.add_subplot(111)
    
    ax.set_xlim((0, 2400))
    ax.set_ylim((0, 2400))
    
    plt.text(1900, 1200, "Nucleolus", ha="center",
            family=font, size=14)
    
    ax.add_collection(collection)
    ax.matshow(im)
    ax.set_axis_off()
    if save:
        fig.savefig('im3.png')
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
