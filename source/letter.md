---
title: letter
date: 2020-05-07
---
Example Python program letter.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt

## Code

Python example

    import numpy as np
    import matplotlib.pyplot as plt
     
    # data to plot
    letter_values = (90, 55, 40, 65, 85, 62, 54, 20, 33, 54)
    letters = {'A': 90, 'B': 55, 'C': 40, 'D': 65, 'E': 85, 'F': 62, 'G': 54, 'H': 20, 'I': 33, 'J': 54}
    
    
    colors = ["#F46716", "#20EA71", "#228FF4", "#F725B8", "#E8F235", 
                "#F9ECC9", "#F9CEAC", "#F7B672", "#F7917B","#FC6B8A"]
    
    # create plot
    
    index = np.arange(len(letters))
    bar_width = 0.35
    opacity = 0.8
     
    i = 0
    for k, v in letters.items():
        plt.barh(k, v, bar_width,
                     alpha=opacity,
                     color=colors[i],
                     label=k)
        i = i + 1
     
     
    plt.ylabel('Letters')
    plt.xlabel('Scores')
    plt.title('Scores by Letters')
    plt.yticks(index, letters)
    plt.legend(loc='lower center', prop={'size':6}, bbox_to_anchor=(0.5,-0.6))
     
    plt.tight_layout(pad=5)
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
