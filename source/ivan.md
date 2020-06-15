---
title: ivan
date: 2020-05-07
---
Example Python program ivan.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import time
* import sys
* import datetime

## Methods

* def write_to_file(file, data):

## Code

Python example

    import matplotlib.pyplot as plt
    import numpy as np
    import time
    import sys
    import datetime
    
    
    def write_to_file(file, data):
    
        file.write(' '.join(map(str, data)) + "\n")
    
    
    file = open("test.txt", "w+")
    file.close()
    
    plt.ion()  # # Note this correction
    fig = plt.figure()
    # plt.axis([0, 1000, 0, 1])
    
    x = []
    y = []
    
    for i in range(1000):
        file = open("test.txt", "a+")
        data = np.random.rand(5)
        with file as f:
            write_to_file(file, data)
        time.sleep(1)
        file = open("test.txt", "r+")
    
        file = open("test.txt", "r")
        data = np.loadtxt(file)
    
        x.append(datetime.datetime.now())
        if np.ndim(data) == 2:
            y.append(data[i][2])
        else:
            y.append(data[2])
    
        file.close()
    
        plt.clf()
        plt.gcf().autofmt_xdate()
        plt.plot(x, y)
    
        plt.show()
        plt.pause(0.0001)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
