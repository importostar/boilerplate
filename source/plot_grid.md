---
title: plot_grid
date: 2020-05-07
---
Example Python program plot_grid.py

## Modules

* import numpy as np
* import pandas as pd
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.gridspec as gridspec
* import itertools as it

## Code

Python example

    %matplotlib inline
    
    
    import numpy as np
    import pandas as pd
    import matplotlib
    import matplotlib.pyplot as plt
    import matplotlib.gridspec as gridspec
    import itertools as it
    
    font = {#'family' : 'normal',
            #'weight' : 'bold',
            'size'   : 20}
    
    matplotlib.rc('font', **font)
    
    fig_conf_curves = plt.figure(figsize=(12, 7))
    gs_conf_curves = gridspec.GridSpec(1, 2)
    axs = [fig_conf_curves.add_subplot(ss) for ss in gs_conf_curves]
    for i in range(10):
        axs[0].plot(conf_curves[i, :, 0], conf_curves[i, :, 1])
        axs[1].plot(conf_curves[i, :26, 0], conf_curves[i, :26, 1])
    for ax in axs:
        ax.set_xlabel('conservation bin')
    axs[0].set_ylabel('BBL')
    axs[0].set_title('conservation bin [0, 100]')
    axs[1].set_title('conservation bin [0, 25]')
    fig_conf_curves.suptitle(#
    """Confidence curves in 10 different sets of shuffle motifs
    B_Atf1_primary, 10 * 10 shuffles, p_value_cutoff=1.3
    """
    )
    gs_conf_curves.tight_layout(fig_conf_curves, rect=[0, 0, 1, 0.88])
    fig_conf_curves.savefig('./compareConfidenceCurves_B_Atf1_primary_curve.png')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
