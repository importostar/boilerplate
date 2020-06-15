---
title: test_matplotlib (1)
date: 2020-05-07
---
Example Python program test_matplotlib (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* import time
* import datetime
* import random
* import math
* import statistics
* import numpy as np
* import matplotlib
* import matplotlib.figure as mfigure
* import matplotlib.ticker as ticker
* from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
* from matplotlib.dates import DayLocator, HourLocator, DateFormatter, drange
* import matplotlib.dates as mdates

## Methods

* def graph():
* def format_date(x, pos=None):
* def pie():
* def bar():
* def simple_bar():

## Code

Python example

    #!/usr/bin/python
    #-*- coding: utf-8 -*-
    import os
    import sys
    import time
    import datetime
    import random
    import math
    import statistics
    import numpy as np
    import matplotlib
    matplotlib.use('Agg')
    import matplotlib.figure as mfigure
    import matplotlib.ticker as ticker
    from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
    from matplotlib.dates import DayLocator, HourLocator, DateFormatter, drange
    import matplotlib.dates as mdates
    
    DIRNAME = os.path.dirname(os.path.abspath(__file__))
    BASENAME = os.path.basename(__file__)
    HERE = os.path.join(DIRNAME, BASENAME)
    get_array = lambda n, i: np.array([j*i+abs(random.random()*i) for j in range(10)])
    A = get_array(10, 1.2)
    B = get_array(10, 2.0)
    np.save(HERE + '.npy', A)
    np.load(HERE + '.npy')
    
    
    def graph():
        fig = mfigure.Figure()
        canvas = FigureCanvas(fig)
        ax = fig.add_subplot(111)
        ax.set_title('hi mom')
        ax.grid(True)
        ax.set_xlabel('time')
        ax.set_ylabel('volts')
    
        C = get_array(10, 3.0)
        D = get_array(10, 1.0)
    
        E = get_array(10, 6.0)
        F = get_array(10, 1.2)
    
        # dates = drange(date1, date2, delta)
        # pylab_examples example code: date_demo_convert.py — Matplotlib 1.5.1 documentation <http://matplotlib.org/examples/pylab_examples/date_demo_convert.html>
        t = [datetime.datetime.now() + datetime.timedelta(days=i) for i in range(10)]
        X_MIN = np.concatenate((A, C, E)).min()
        X_MAX = np.concatenate((A, C, E)).max()
        Y_MIN = np.concatenate((B, D, F)).min()
        Y_MAX = np.concatenate((B, D, F)).max()
        # ax.set_xlim(X_MIN, X_MAX)
        ax.set_ylim(Y_MIN, Y_MAX)
    
        years = mdates.YearLocator()   # every year
        months = mdates.MonthLocator()  # every month
        yearsFmt = mdates.DateFormatter('%Y-%m-%d')
        
        def format_date(x, pos=None):
            s = t[pos].strftime('%Y-%m-%d')
            print(s)
            return s
    
        # ax.xaxis.set_major_locator(years)
        ax.xaxis.set_major_formatter(yearsFmt)
        # ax.xaxis.set_major_formatter(ticker.FuncFormatter(format_date))
        # ax.xaxis.set_minor_locator(months)
        fig.autofmt_xdate()
    
        ax.plot(t, B, '-o', label='a', ms=20, lw=2, alpha=0.7, mfc='orange')
        ax.plot(t, D, '-o', label='b', ms=20, lw=2, alpha=0.7, mfc='red')
        ax.plot(t, F, '-o', label='c', ms=20, lw=2, alpha=0.7, mfc='blue')
        legend = ax.legend(loc='upper center', shadow=True, fontsize='x-large')
        fig.savefig(HERE + '.png')
    
        return 0
    
    
    def pie():
        fig = mfigure.Figure()
        dpi = 96
        fig.set_size_inches(300/dpi, 300/dpi)
        canvas = FigureCanvas(fig)
        ax = fig.add_subplot(111)
        labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
        sizes = [15, 30, 45, 10]
        colors = ['yellowgreen', 'gold', 'lightskyblue', 'lightcoral']
        explode = (0, 0.1, 0, 0)  # only "explode" the 2nd slice (i.e. 'Hogs')
        
        ax.pie(sizes, explode=explode, labels=labels, colors=colors,
                autopct='%1.1f%%', shadow=True, startangle=90)
        fig.savefig(HERE + ".bar.png")
    
    
    def bar():
        fig = mfigure.Figure()
        canvas = FigureCanvas(fig)
        ax = fig.add_subplot(111)
        ax.set_title('hi mom')
        ax.grid(True)
        ax.set_xlabel('time')
        ax.set_ylabel('volts')
    
        width = 0.2
        y = [random.randint(0, 30) for i in range(5)]
        x = np.arange(5)
        a1 = ax.bar(x, y, width=width, color='r',label='bars1')
        a2 = ax.bar(x + width, y, width, color='b', label='bars2')
        ax.set_xticklabels(('A', 'B', 'C', 'D', 'E'))
        ax.legend((a1, a2), ['1', '2'])
    
        fig.savefig(HERE + ".bar.png")
        return 0
    
    
    def simple_bar():
        fig = mfigure.Figure()
        canvas = FigureCanvas(fig)
        ax = fig.add_subplot(111)
        ax.set_title('hi mom')
        ax.grid(True)
        ax.set_xlabel('time')
        ax.set_ylabel('volts')
    
        width = 0.1
        y = np.array([1, 2, 3])
        x = np.arange(3)
        print(x)
        print(y)
        a1 = ax.bar(x, y, width=width, color='r', label='bars1')
        labels = ('A', 'B', 'C')
        ax.set_xticks(x)
        ax.set_xticklabels(labels)
        ax.legend((a1,), ['1'])
    
        fig.savefig(HERE + ".bar.png")
        return 0
    
    
    
    if __name__ == '__main__':
        exec(sys.argv[1])
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
