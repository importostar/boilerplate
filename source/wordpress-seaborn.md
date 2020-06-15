---
title: wordpress seaborn
date: 2020-05-07
---
Example Python program wordpress-seaborn.py

## Modules

* import seaborn as sns
* import matplotlib.pyplot as plt

## Code

Python example

    import seaborn as sns
    import matplotlib.pyplot as plt
    
    #Set theme and size, remove axis titles
    sns.set_style("whitegrid")
    sns.set_context({"figure.figsize": (17, 6)}) #Passing in matplotlib commands directly
    
    #Plot data
    #Use dataset.index as my x_order, to ensure proper ordering by using numeric series
    sns_views = sns.barplot(dataset.Month, "Views", data = dataset, color = "#278DBC", dropna = False, ci=None, x_order=dataset.Month)
    
    #Hack to use matplotlib directly to set bar width, since Seaborn doesn't currently allow for setting bar width
    plotvisitors2= dataset.Visitors.plot(kind='bar', width = .5, color =  '#000099', clip_on=False, grid=False)
    plotvisitors2.yaxis.grid(color='gray', linestyle='solid')
    plotvisitors2.set_axisbelow(True)
    
    #Remove borders around graph, remove axis labels
    #Needs to be called after plot generated or it doesn't work
    sns.despine(left=True) 
    sns.axlabel("", "") 
    
    #Set custom labels for chart
    sns_views.set_xticklabels(dataset.Month_, rotation=0)
    
    #Create legend using same matplotlib code from above
    sns_views.legend([views, visitors], ['Views', 'Visitors'], loc=1, ncol = 2)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
