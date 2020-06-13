---
title: chart_tut
date: 2020-05-07
---
Example Python program chart_tut.py

## Modules

* # organize imports
* import numpy as np
* import matplotlib.pyplot as plt

## Code

Python example

    ##################################
    # matplotlib basics - 2 
    ##################################
    
    # organize imports
    import numpy as np
    import matplotlib.pyplot as plt
    
    # ---Random dataset---
    values = [55, 30, 6, 5, 4]
    X = np.random.randn(1000)
    Y = np.random.randn(1000)
    
    # assign colors to each category
    colors = ['b', 'g', 'r', 'c', 'y']
    
    # explode to show any of the categories
    explode = [0, 0, 0, 0, 0.2]
    
    # assign labels to each category
    labels = ['Dogs', 'Cats', 'Fish', 'Rabbits', 'Elephants']
    
    # plot the pie chart
    plt.figure("Sample Pie chart")
    plt.pie(values, colors=colors, labels=labels, explode=explode, autopct='%1.1f%%', shadow=True, startangle=80)
    plt.title('Pet Ownership')
    plt.axis('equal')
    
    # save it to a file
    plt.savefig('pie.png', format='png')
    
    # plot the bar chart
    plt.figure("Sample Bar chart")
    plt.bar(range(0,5), values, color = colors)
    plt.title('Pet Ownership')
    axes = plt.axes()
    axes.set_xticklabels(labels)
    
    # save it to a file
    plt.savefig('bar.png', format='png')
    
    # plot the scatter plot
    plt.figure("Sample scatter plot")
    plt.scatter(X,Y)
    plt.title('A sample plot')
    
    # save it to a file
    plt.savefig('scatter.png', format='png')
    
    # display the charts
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
