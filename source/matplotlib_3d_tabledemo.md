---
title: matplotlib_3d_tabledemo
date: 2020-05-07
---
Example Python program matplotlib_3d_tabledemo.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt

## Code

Python example

    import numpy as np
    import matplotlib.pyplot as plt
    
    data = np.loadtxt(open("data.csv","rb"),delimiter=",",skiprows=0)
    
    # data = [[ 66386, 174296,  75131, 577908,  32015],
    #         [ 58230, 381139,  78045,  99308, 160454],
    #         [ 89135,  80552, 152558, 497981, 603535],
    #         [ 78415,  81858, 150656, 193263,  69638],
    #         [139361, 331509, 343164, 781380,  52269]]
    print(data)
    columns = np.arange(0,len(data[0]*5),5)
    rows =np.arange(0,len(data[1]))
    
    values = np.arange(0, 9, 0.1)
    value_increment = 1
    
    # Get some pastel shades for the colors
    colors = plt.cm.BuPu(np.linspace(0, 0.5, len(rows)))
    n_rows = len(data)
    
    index = np.arange(len(columns))
    bar_width = 0.1
    
    # Initialize the vertical-offset for the stacked bar chart.
    y_offset = np.zeros(len(columns))
    
    # Plot bars and create text labels for the table
    cell_text = []
    for row in range(n_rows):
        plt.bar(index, data[row], bar_width, bottom=y_offset, color=colors[row])
        y_offset = y_offset + data[row]
        cell_text.append(['%1.1f' % (x / 1000.0) for x in y_offset])
    # Reverse colors and text labels to display the last value at the top.
    colors = colors[::-1]
    cell_text.reverse()
    
    # Add a table at the bottom of the axes
    the_table = plt.table(cellText=cell_text,
                          rowLabels=rows,
                          rowColours=colors,
                          colLabels=columns,
                          loc='bottom')
    
    # Adjust layout to make room for the table:
    plt.subplots_adjust(left=0.2, bottom=0.2)
    
    plt.ylabel("Loss in ${0}'s".format(value_increment))
    plt.yticks(values * value_increment, ['%d' % val for val in values])
    plt.xticks([])
    plt.title('Loss by Disaster')
    
    plt.show()
    print("finish")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
