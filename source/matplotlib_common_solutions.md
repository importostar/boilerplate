---
title: matplotlib_common_solutions
date: 2020-05-07
---
Example Python program matplotlib_common_solutions.py

## Modules

* import matplotlib

## Code

Python example

    import matplotlib
    # To solve remote session issues:
    matplotlib.use("Agg")
    
    # To make fonts editable (Type 3 to Type 2):
    matplotlib.rcParams['pdf.fonttype'] = 42
    matplotlib.rcParams['ps.fonttype'] = 42
    plt.savefig("foo.pdf", transparent = True) # PDF is the best.
    
    # subplots settings:
    fig = plt.figure(figsize=(10, 10))
    ax0 = fig.add_subplot(211)
    ax1 = fig.add_subplot(212)
    ## axis ticks and labels of axes
    ax0.set_xticks([1, 2, 3, 4, 5])
    ax0.set_xticklabels(["1", "2", "3", "4", "5"], fontsize=20)
    ax0.tick_params(axis="both", width=2)
    ## axis visibility and width:
    ax0.spines['right'].set_visible(False)
    ax0.spines['left'].set_visible(False)
    ax0.spines['top'].set_lw(2)
    ax0.spines['bottom'].set_lw(2)
    ## x and y labels:
    ax1.set_xlabel("XXXX", fontsize=34)
    ## x & y limitation:
    ax1.set_xlim(150.68e6, 153.95e6)
    
    # adjust subplots:
    plt.subplots_adjust(hspace=0.35, left=0.15, right=0.99)
    
    # to set equal scale:
    plt.gca().set_aspect('equal', adjustable='box')
    
    # draw verticle lines:
    ax1.vlines(151.68e6, 0, 0.05, colors="g", linestyles="dashed", linewidth=2) # OR plt.vlines

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
