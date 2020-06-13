---
title: mpf ohlc_filter
date: 2020-05-07
---
Example Python program mpf-ohlc_filter.py

## Modules

* import pandas as pd
* import matplotlib.pyplot as plt
* import matplotlib.dates as mdates

## Methods

* def format_data(data, colnames={'open':'Open', 'high':'High', 'low':'Low', 'close':'Close'}, index_as_datetime=True):

## Code

Python example

    import pandas as pd
    import matplotlib.pyplot as plt
    import matplotlib.dates as mdates
    
    def format_data(data, colnames={'open':'Open', 'high':'High', 'low':'Low', 'close':'Close'}, index_as_datetime=True):
        
        # We need to exctract the OHLC prices into a list of lists:
        dvalues = data[[colnames['open'], colnames['high'], colnames['low'], colnames['close']]].values.tolist()
    #     dvalues = data[['Open', 'High', 'Low', 'Close']].values.tolist()
        
        if index_as_datetime:
            # Dates in our index column are in datetime format, we need to comvert them 
            # to Matplotlib date format (see https://matplotlib.org/3.1.1/api/dates_api.html):
            pdates = mdates.date2num(data.index)
        else:
            # If dates in our index column are strings instead of datetime objects, we should use:
            pdates = mdates.datestr2num(data.index)
    
        # We prepare a list of lists where each single list is a [date, open, high, low, close] sequence:
        ohlc = [ [pdates[i]] + dvalues[i] for i in range(len(pdates)) ]
        
        return ohlc

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
