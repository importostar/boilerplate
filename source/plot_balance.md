---
title: plot_balance
date: 2020-05-07
---
Example Python program plot_balance.py

## Modules

* import pandas as pd
* from pandas.plotting import register_matplotlib_converters
* import numpy as np
* import datetime as dt
* import matplotlib
* import matplotlib.pyplot as plt
* import argparse

## Code

Python example

    import pandas as pd
    from pandas.plotting import register_matplotlib_converters
    register_matplotlib_converters()
    import numpy as np
    import datetime as dt
    
    import matplotlib
    import matplotlib.pyplot as plt
    
    import argparse
    
    parser = argparse.ArgumentParser()
    parser.add_argument('--input', type=str, help='filename of input CSV data')
    parser.add_argument('--degree', type=int, default=1, help='degree of polynomial fitting)')
    opt = parser.parse_args()
    
    df = pd.read_csv(opt.input, dayfirst=True, parse_dates=True, header=None)
    dates = np.flip(df.values[:,0], axis=0)
    values = np.flip(df.values[:,1], axis=0).astype(float)
    datetimes = [dt.datetime.strptime(d,'%d/%m/%Y').date() for d in dates]
    dates = matplotlib.dates.date2num(datetimes)
    poly = np.polynomial.polynomial.Polynomial.fit(dates, values, opt.degree)
    der = poly.deriv()
    
    fig, ax1 = plt.subplots()
    ax1.plot_date(dates, values, 'b-')
    ax1.plot_date(dates, poly(dates), 'r-')
    plt.xticks(rotation=-45)
    ax1.set_xlabel('Month')
    ax1.set_ylabel('Balance', color='b')
    ax1.tick_params('y', colors='b')
    ax2 = ax1.twinx()
    ax2.plot_date(dates, 30 * der(dates), 'g-')
    ax2.tick_params('y', colors='g')
    ax2.set_ylabel('Monthly saving', color='g')
    fig.tight_layout()
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
