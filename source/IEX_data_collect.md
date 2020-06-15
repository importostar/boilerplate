---
title: IEX_data_collect
date: 2020-05-07
---
Example Python program IEX_data_collect.py

## Modules

* #import packages for use later in the HMM code
* import pandas as pd
* import sklearn.mixture as mix
* import numpy as np
* import scipy.stats as scs
* import datetime as dt
* import matplotlib as mpl
* from matplotlib import cm
* import matplotlib.pyplot as plt
* from matplotlib.dates import YearLocator, MonthLocator
* import seaborn as sns
* from iex import Stock

## Code

Python example

    #import packages for use later in the HMM code
    
    import pandas as pd
    import sklearn.mixture as mix
    
    import numpy as np
    import scipy.stats as scs
    
    import datetime as dt
    
    import matplotlib as mpl
    from matplotlib import cm
    import matplotlib.pyplot as plt
    from matplotlib.dates import YearLocator, MonthLocator
    %matplotlib inline
    
    import seaborn as sns
    
    from iex import Stock
    
    ticker = ["SPY"]
    all_historic_data = pd.DataFrame()
    
    for t in ticker:
        ticker_data = Stock(t).chart_table(range="5y")
        
        ticker_data_clean = ticker_data[["date", "close", "high", "low"]]
        ticker_data_clean["date"] = pd.to_datetime(ticker_data_clean["date"])
        ticker_data_clean.insert(1, "ticker", t)
        ticker_data_clean["return"] = ticker_data_clean["close"].pct_change()
        
        ticker_data_clean["range"] = (ticker_data_clean["high"]/ticker_data_clean["low"])-1
        del ticker_data_clean["high"]
        del ticker_data_clean["low"]
        ticker_data_clean.dropna(how="any", inplace=True)
    
        
        all_historic_data = pd.concat([all_historic_data, ticker_data_clean])
    
    all_historic_data.head()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
