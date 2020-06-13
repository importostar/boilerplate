---
title: emojis_plotted_complete_code
date: 2020-05-07
---
Example Python program emojis_plotted_complete_code.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib, mplcairo
* import matplotlib.pyplot as plt, numpy as np
* from matplotlib.font_manager import FontProperties

## Code

Python example

    # Set the backend to use mplcairo 
    import matplotlib, mplcairo
    print('Default backend: ' + matplotlib.get_backend()) 
    matplotlib.use("module://mplcairo.macosx")
    print('Backend is now ' + matplotlib.get_backend())
    
    # IMPORTANT: Import these libraries only AFTER setting the backend
    import matplotlib.pyplot as plt, numpy as np
    from matplotlib.font_manager import FontProperties
    
    # Load Apple Color Emoji font 
    prop = FontProperties(fname='/System/Library/Fonts/Apple Color Emoji.ttc')
    
    # Set up plot
    freqs = [301, 96, 53, 81, 42]
    labels = ['😊', '😱', '😂', '😄', '😛']
    plt.figure(figsize=(12,8))
    p1 = plt.bar(np.arange(len(labels)), freqs, 0.8, color="lightblue")
    plt.ylim(0, plt.ylim()[1]+30)
    
    # Make labels
    for rect1, label in zip(p1, labels):
        height = rect1.get_height()
        plt.annotate(
            label,
            (rect1.get_x() + rect1.get_width()/2, height+5),
            ha="center",
            va="bottom",
            fontsize=30,
            fontproperties=prop
        )
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
