---
title: TTB03 ohlc_data (1)
date: 2020-05-07
---
Example Python program TTB03-ohlc_data (1).py

## Modules

* import pandas as pd
* import matplotlib.pyplot as plt
* import matplotlib.dates as mdates

## Code

Python example

    import pandas as pd
    import matplotlib.pyplot as plt
    import matplotlib.dates as mdates
    
    # Loading data into dataframe:
    datafile = 'SPY.csv'
    data = pd.read_csv(datafile, index_col = 'Date')
    # Converting the dates from string to datetime format:
    data.index = pd.to_datetime(data.index)
    
    # We need to exctract the OHLC prices into a list of lists:
    dvalues = data[['Open', 'High', 'Low', 'Close']].values.tolist()
    
    # Dates in our index column are in datetime format, we need to comvert them 
    # to Matplotlib date format (see https://matplotlib.org/3.1.1/api/dates_api.html):
    pdates = mdates.date2num(data.index)
    
    # If dates in our index column are strings instead of datetime objects, we should use:
    # pdates = mpl.dates.datestr2num(data.index)
    
    # We prepare a list of lists where each single list is a [date, open, high, low, close] sequence:
    ohlc = [ [pdates[i]] + dvalues[i] for i in range(len(pdates)) ]

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
