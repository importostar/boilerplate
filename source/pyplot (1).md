---
title: pyplot (1)
date: 2020-05-07
---
Example Python program pyplot (1).py

## Modules

* import matplotlib
* import matplotlib.pyplot as plt

## Code

Python example

    # -----------------------------------
    # Standard Pyplot Configuration
    # -----------------------------------
    
    import matplotlib
    matplotlib.use("Qt5Agg")  # Qt5 backend works well on Windows and macOS
    import matplotlib.pyplot as plt
    
    fig = plt.figure()  # params: (num=1, figsize=(10, 4), dpi=300) - figsize in inches
    
    # Useful arguments:
    #	alpha = {float}
    #	color = {color}
    #	label = {object}	-> Label for auto legend creation
    #	linestyle = {'-', '--', '-.', ':', '', (offset, on-off-seq), ...}
    #	linewidth = {float}
    
    # For [fmt]: https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot
    # For **kwargs: https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D
    [lines] = plt.plot([x], y, [fmt], data=None, **kwargs)  # params: [fmt]: format string -> [color][marker][line]
    
    plt.close()  # params: None->current, handle, fig_num (e.g. 1,2,..)
    
    # -----------------------------------
    # Pandas Plotting
    # -----------------------------------
    
    # Easy way to plot Pandas dataframes
    lines = plt.plot('xlabel', 'ylabel', data=obj)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
