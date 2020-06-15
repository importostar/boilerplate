---
title: sample (1)
date: 2020-05-07
---
Example Python program sample (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import matplotlib.animation as animation
* import serial
* import platform
* import time
* import datetime
* import csv
* import re

## Methods

* def update(data):
* def run(data):
* def data_gen():

## Code

Python example

    import numpy as np
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    import matplotlib.animation as animation
    import serial
    import platform
    import time
    import datetime
    import csv
    import re
    print("Python version: " + platform.python_version())
    print("matplotlib version: " + mpl.__version__)
    
    fig, ax = plt.subplots()
    line, = ax.plot(np.random.rand(10))
    ax.set_ylim(-.1, .08)
    xdata, ydata = [0]*100, [0]*100
    SerialIn = serial.Serial("com4",115200)
    FILE = open('Pressure ' + time.strftime("%Y-%m-%d %H:%M") + '.csv','a')
    
    pattern = re.compile( r'([0-9 .+-]*)' ) #Added
    
    
    
    def update(data):
        line.set_ydata(data)
        return line,
    
    def run(data):
        global xdata, ydata
        x,y = data
        if (x == 0):
            xdata = [0]*100
            ydata = [0]*100
        del xdata[0]
        del ydata[0]
        xdata.append(x)
        ydata.append(y)
        line.set_data(xdata, ydata)
        return line,
    
    def data_gen():
        x = 10
        while True:
            if (x >= 9):
                x = 0
            else:
                x += 0.1
    
            SerialIn.write(b"P\r")
            try:
                inRaw = re.search( pattern, 
    SerialIn.read(SerialIn.in_waiting).decode('utf-8') ).group(0)
                inInt = float(inRaw)
                TIME = time.strftime('%H:%M:%S')
                FILE.write("{0},{1}\r".format(TIME, inInt))
                FILE.flush()
                print('['+time.strftime('%H:%M:%S')+']',inInt)
                time.sleep(1-time.time()%1)
    
            except:
               inInt = 0
    
            yield x, inInt
    
    ani = animation.FuncAnimation(fig, run, data_gen, interval=0, blit=True)
    
    plt.show()
    
    
    SerialIn.close()
    FILE.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
