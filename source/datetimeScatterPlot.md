---
title: datetimeScatterPlot
date: 2020-05-07
---
Example Python program datetimeScatterPlot.py

## Modules

* import matplotlib.pyplot as plt
* from matplotlib import dates
* import datetime
* from pandas.plotting import register_matplotlib_converters

## Code

Python example

    import matplotlib.pyplot as plt
    from matplotlib import dates
    import datetime
    
    from pandas.plotting import register_matplotlib_converters
    register_matplotlib_converters()
    
    # TODO: Turn this bad boy into a function
    
    # Raw data example (Format will vary)
    data = ['2018-08-05 06:39:51', '2018-08-05 11:22:55', '2018-08-05 11:28:17', '2018-08-05 11:47:40', '2018-08-05 11:50:24', '2018-08-05 11:57:43', '2018-08-05 11:58:01', '2018-08-05 11:58:07', '2018-08-05 11:58:34', '2018-08-05 12:15:01']
    
    # convert data to list of datetime objects; pay attention to format
    lodt = [datetime.datetime.strptime(dt, '%Y-%m-%d %H:%M:%S') for dt in data]
    
    # Build the plot axis from the dataset
    x_axis, y_axis = zip(*[(itm.date(), itm.time()) for itm in lodt])
    
    # Build the plot
    # Add multiple plot calls for different data
    plt.plot( x_axis, y_axis, 'b.', markersize=2 ) 
    ax = plt.gcf().axes[0]
    ax.xaxis.set_major_formatter(dates.DateFormatter('%Y-%m-%d'))
    ax.set_ylim(["00:00:00", "23:59:59"])
    ax.set_xlim(["2018-08-03", "2018-08-07"]) # Change to fit formatting
    plt.gcf().autofmt_xdate(rotation=25) # fix axis formatting
    plt.title('Date time scatter plot')
    plt.ylabel('Time')
    plt.xlabel('Date')
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
