---
title: question
date: 2020-05-07
---
Example Python program question.py

## Modules

* from __future__ import division
* import numpy as np
* from numpy import log
* import matplotlib.pyplot as plt
* import datetime
* import matplotlib.dates as mdates
* import matplotlib.axis as ax
* import pandas as pd
* import datetime as dt

## Code

Python example

    
    
    from __future__ import division
    import numpy as np
    from numpy import log
    import matplotlib.pyplot as plt
    import datetime
    import matplotlib.dates as mdates
    import matplotlib.axis as ax
    import pandas as pd
    import datetime as dt
    # %matplotlib inline
    
    #load data
    vac = pd.read_csv('/Users/freda/Copy/vacancy1.csv')
    
    #define what to plot
    year = vac['Year']
    vacancies = vac['Vacancies']
    price = vac['Price_index']
    
    fig = plt.figure(figsize=(20, 10))
    ax = fig.add_subplot(111)
    ax2 = ax.twinx()
    # plt.xticks(year[1:12])
    #ax.xaxis_date()
    plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y'))
    # plt.gca().xaxis.set_major_locator()
    # ax2.xaxis_date()
    #plt.xticks(ts1[0::12])
    ax.set_xlabel("Year")
    ax2.set_ylim(0, 270)
    ax.plot(year, vacancies, '-', label = 'vacancies')
    ax2.plot(year, price, '-r', label = 'price')
    ax.grid()
    ax.legend()
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
