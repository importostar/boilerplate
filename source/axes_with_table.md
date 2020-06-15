---
title: axes_with_table
date: 2020-05-07
---
Example Python program axes_with_table.py

## Modules

* from collections import OrderedDict
* import matplotlib.pyplot as plt
* import numpy as np
* from mpl_toolkits.axes_grid1 import make_axes_locatable
* from matplotlib.table import table

## Code

Python example

    #!/usr/bin/env python
    
    from collections import OrderedDict
    
    import matplotlib.pyplot as plt
    import numpy as np
    from mpl_toolkits.axes_grid1 import make_axes_locatable
    from matplotlib.table import table
    
    fig = plt.figure()
    fig.suptitle("This is a test Figure", fontsize=20)
    fig.patch.set_facecolor('red')
    fig.subplots_adjust(top=0.85)
    
    ax1 = fig.add_subplot(111)
    X, Y = np.meshgrid(np.linspace(-5, 5, 128),
                       np.linspace(-5, 5, 128))
    
    tmp = ax1.contourf(X, Y, np.exp(abs(X + 1j * Y)))
    ax1.set_aspect(1)
    ax1.set_xlabel('$x_{TB}$ [nm]')
    ax1.set_ylabel('$y_{TB}$ [nm]')
    divider = make_axes_locatable(ax1)
    # this code is from
    # http://matplotlib.org/mpl_toolkits/axes_grid/users/overview.html#axes-grid1
    cax = divider.append_axes("top", size="5%", pad=0.05)
    cb = fig.colorbar(tmp, cax=cax, orientation='horizontal')
    cb.ax.xaxis.set_ticks_position('top')
    cax.set_xlabel("Current")
    cb.ax.xaxis.set_label_position('top')
    
    ax2 = divider.append_axes('right', size='65%', pad=0.15)
    ax2.set_xticks([])
    ax2.set_yticks([])
    for m in ['left', 'right', 'top', 'bottom']:
        ax2.spines[m].set_visible(False)
    # in qt windows use this
    # ax2.patch.set_facecolor(fig.patch.get_facecolor())
    
    mydata = OrderedDict()
    mydata['center x'] = 2.3423
    mydata['center y'] = 110.2
    mydata['blur x'] = 0.2
    mydata['blur y'] = 24.44
    mydata['amplitude'] = -125.2225
    mydata['offset'] = 0.55
    celldata = [[val[0], '{0:g}'.format(val[1])] for val in mydata.items()]
    
    the_table = table(ax2,
                      cellText=celldata,
                      colLabels=['', 'fit parameters'],
                      loc='upper center')
    the_table.AXESPAD = 0.0
    
    # custom axes for colorbar (first try)
    # rect = [0.6, 0.15, 0.02, 0.4]
    # axcb = fig.add_axes(rect, axisbg='g')
    # axcb.set_xticks([])
    # axcb.set_yticks([])
    # for m in ['left', 'right', 'top', 'bottom']:
    #     axcb.spines[m].set_visible(False)
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
