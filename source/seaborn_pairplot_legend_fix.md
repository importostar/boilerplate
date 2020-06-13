---
title: seaborn_pairplot_legend_fix
date: 2020-05-07
---
Example Python program seaborn_pairplot_legend_fix.py

## Modules

* import seaborn as sns

## Code

Python example

    import seaborn as sns
    
    sns.set()
    
    # turn on interactive mode, avoid-blocking
    sns.plt.ion()
    
    # take iris scatterplot matrix as an example
    iris = sns.load_dataset("iris")
    
    # plot with conda bulit matplotlib-1.5.3-np111py35_1 and seaborn-0.7.1-py35_0
    # legend is crushing on the right edge of subplots
    sns.pairplot(iris, hue="species")
    
    # investigating the right margin of subplot parameters
    sns.plt.gcf().subplotpars.right
    # will return: 0.98875156054931335
    # while the documented default value is 0.9, according to 
    # http://matplotlib.org/api/figure_api.html#matplotlib.figure.SubplotParams
    # the value of right margin might be changed by matplotlib.pyplot.tight_layout()?
     
    # reset the right margin of subplot to its documented default value will temporarily solve the crushing issue.
    sns.plt.gcf().subplots_adjust(right=0.9) # you can further reduce the value to separate legend and subplots.
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
