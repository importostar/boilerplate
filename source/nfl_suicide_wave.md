---
title: nfl_suicide_wave
date: 2020-05-07
---
Example Python program nfl_suicide_wave.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib

## Code

Python example

    # inspired by:
    # http://stackoverflow.com/questions/33019879/hierarchic-pie-donut-chart-from-pandas-dataframe-using-bokeh-or-matplotlib
    
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib
    matplotlib.style.use('ggplot')
    %matplotlib inline
    
    correct_per = [0.875, 0.636, 0.500, 0.500, 0.583, 0.556, 0.625]
    correct_per = [[i] for i in correct_per]
    
    # "compounded" correct picks
    for i in range(1, len(correct_per)):
        correct_per[i][0] = correct_per[i][0] * correct_per[i-1][0]
        
    WL_pairs = [[i[0], 1.0-i[0]] for i in correct_per]
    
    for i in range(len(WL_pairs)):
        if i == 0:
            WL_pairs[i].append(0)
        else:
            WL_pairs[i].append(np.sum(WL_pairs[i-1][1:]))
            WL_pairs[i][1] -= WL_pairs[i][2]
        
    print WL_pairs
    print [np.sum(i) for i in WL_pairs]
    
    colors = ['dodgerblue', 'darkblue', 'black']
    
    plt.figure(figsize=(10,10))
    plt.pie(WL_pairs[-1], colors=colors)
    
    ax = plt.gca()
    
    for i in np.arange(len(WL_pairs)-2,-1,-1):
        ax.pie(WL_pairs[i], colors=colors, 
               radius=np.float(i+1)/float(len(WL_pairs)))
    
    
    ax.set_aspect('equal')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
