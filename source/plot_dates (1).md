---
title: plot_dates (1)
date: 2020-05-07
---
Example Python program plot_dates (1).py

## Modules

* import pandas as pd
* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import matplotlib.dates as mdates

## Code

Python example

    import pandas as pd
    
    # Visualisation
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    import matplotlib.dates as mdates
    
    # Configure visualisations
    %matplotlib inline
    mpl.style.use( 'ggplot' )
    sns.set_style( 'white' )
    pylab.rcParams[ 'figure.figsize' ] = 30 , 12
    
    # set x and y values, x must be a datetime
    ax = df.plot(x='x', y='y')
    
    # set a locator, set interval
    # MicrosecondLocator: locate microseconds
    # SecondLocator: locate seconds
    # MinuteLocator: locate minutes
    # HourLocator: locate hours
    # DayLocator: locate specified days of the month
    # WeekdayLocator: Locate days of the week, e.g., MO, TU
    # MonthLocator: locate months, e.g., 7 for july
    # YearLocator: locate years that are multiples of base
    ax.xaxis.set_major_locator(mdates.MinuteLocator(interval=5))
    
    # set formatter, see http://strftime.org/
    ax.xaxis.set_major_formatter(mdates.DateFormatter('%H-%M-%S'))
    
    plt.title('x over time');
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
