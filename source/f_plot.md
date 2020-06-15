---
title: f_plot
date: 2020-05-07
---
Example Python program f_plot.py

## Modules

* # import numpy as np
* # import matplotlib.pyplot as plt

## Methods

* def f_plot((v_x, v_y, s_Title, s_LabelX, s_LabelY):

## Code

Python example

    # Required libraries
    # import numpy as np
    # import matplotlib.pyplot as plt
    
    def f_plot((v_x, v_y, s_Title, s_LabelX, s_LabelY):
      # Inputs
      # v_x (numpy vector)		: data for x-axis
      # v_y (numpy vector)		: data for y-axis
      # s_title (string)		: title of the figure 
      # s_label_x (string)		: x-label name
      # s_label_y (string)		: y-label name
      # s_legend (string tuples): legends for data
    
      # Setup of figure parameters
      fig, axs = plt.subplots(1, 1, sharex = True, sharey = False, figsize = (14, 7))
    
      # Plotting data (v_X, v_Y)
      axs.plot(v_x, v_y, 'g-')
    
      # Setup min/max values in x-axis
      axs.axis(xmin = 0, xmax = np.amax(v_X))
    
      # Configure grid in figure
      axs.minorticks_on()
      axs.grid(b = True, which = 'minor', color = '#999999', linestyle = '-', alpha = 0.2)
    
      # Setup axis, legend and title strings
      axs.set(xlabel = s_label_x, ylabel = s_label_y)
      fig.legend(s_legend, loc = 'upper right', shadow = True, fancybox = True)
      fig.suptitle(s_Title, fontsize=16)
    
      # Show figure
      plt.show()
      pass

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
