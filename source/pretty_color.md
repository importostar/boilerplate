---
title: pretty_color
date: 2020-05-07
---
Example Python program pretty_color.py

## Modules

* import itertools
* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib

## Code

Python example

    import itertools
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib
    
    # usage
    # pretty_color = itertools.cycle[tableau20]
    # pretty_color.next[]
    
    tableau20 = np.array([[31, 119, 180], [174, 199, 232], [255, 127, 14], [255, 187, 120],
                 [44, 160, 44], [152, 223, 138], [214, 39, 40], [255, 152, 150],
                 [148, 103, 189], [197, 176, 213], [140, 86, 75], [196, 156, 148],
                 [227, 119, 194], [247, 182, 210], [127, 127, 127], [199, 199, 199],
                 [188, 189, 34], [219, 219, 141], [23, 190, 207], [158, 218, 229]]) * 1. / 255
    
    tableau10 = np.array([[(31,119,180), (255,127,14),(44,160,44), (214,39,40), (148,103,189),
    (140,86,75), (227,119,194),(127,127,127),(188,189,34),(23,190,207)]]) * 1. / 255
    
    matplotlib.rcParams.update({'font.size': 22})
    matplotlib.rcParams['figure.figsize'] = 10, 8

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
