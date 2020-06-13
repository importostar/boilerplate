---
title: covid19 small multiples (1)
date: 2020-05-07
---
Example Python program covid19-small-multiples (1).py

## Modules

* import math
* import pandas as pd
* import numpy as np
* import seaborn as sns
* import matplotlib as mpl
* from matplotlib import pyplot as plt
* from matplotlib.colors import ListedColormap
* from matplotlib.patches import Patch
* from IPython.display import HTML
* from IPython.display import clear_output
* from datetime import datetime
* # import some data - this is from the NY Times

## Methods

* def round_up(n, decimals=0):

## Code

Python example

    # covid19-small-multiples
    
    import math
    import pandas as pd
    import numpy as np
    import seaborn as sns
    
    # setup for plotting
    import matplotlib as mpl
    from matplotlib import pyplot as plt
    from matplotlib.colors import ListedColormap
    from matplotlib.patches import Patch
    
    from IPython.display import HTML
    from IPython.display import clear_output
    
    from datetime import datetime
    
    plt.style.use('fivethirtyeight')
    
    #%matplotlib inline
    #%config InlineBackend.figure_format = 'retina'
    
    # Increase default figure and font sizes for easier viewing.
    plt.rcParams['figure.figsize'] = (8, 6)
    plt.rcParams['font.size'] = 14
    
    # define a custom function for rounding up
    def round_up(n, decimals=0):
        multiplier = 10 ** decimals
        return math.ceil(n * multiplier) / multiplier
    
    
    # import some data - this is from the NY Times
    url = 'https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv'
    us_states = pd.read_csv(url, parse_dates=['date'])
    
    # Replaces spaces with "-" and make column names lowercase
    # NOTE: combine into lowercase and underscore w/ one line!!
    us_states.columns = us_states.columns.str.lower().str.replace(" ", "-")
    
    # put the states in a unique list
    list_states = us_states['state'].sort_values().unique()
    
    # most recent date in the dataframe
    mydate = us_states.date.max()
    
    # convert to a string for use in filename later
    str_mydate = mydate.strftime("%Y-%m-%d")
    
    
    # SMALL MULTIPLES - All States
    
    # surpress SettingWithCopyWarning
    pd.set_option('mode.chained_assignment',None)
    
    # delete the states that won't have enough data to plot
    list_states = list_states[(list_states != 'Alaska') & (list_states != 'Hawaii') & (list_states != 'Montana') 
                             & (list_states != 'Northern Mariana Islands') & (list_states != 'Virgin Islands')
                             & (list_states != 'Wyoming')]
    
    num = 0
    ncols = 5
    nrows = int(np.ceil(len(list_states) / ncols))
    
    fig, axes = plt.subplots(nrows = nrows, ncols = ncols, figsize = (20, nrows*3))
    
    # loop through states and plot
    for state in list_states:
        df = us_states[(us_states.state == state)]
    
        # add calculated cases per day column (NOTE: SettingWithCopyWarning)
        df['cases_per_day'] = df.cases.diff()
    
        # add calculated case-rate column (NOTE: SettingWithCopyWarning)
        df['case_rate'] = np.round(df.cases_per_day.rolling(window=7).mean(),0)
    
        # mask for case_rate >= 30 days
        df = df[(df.case_rate >= 30)]
    
        # maximum y-axis, calculated
        max_y = round_up(df.case_rate.max(), -2)
    
        # interval for y-axis
        interval_y = max_y / 4
    
        # find the right spot on the plot
        num+=1
        plt.subplot(nrows, ncols, num)
        
        ax = df.case_rate.plot(kind="line", xticks = (),
                      title = state,
                      ylim = (0, max_y), yticks=(0, interval_y, 2*interval_y, 3*interval_y, 4*interval_y));
    
        ax.yaxis.set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.0f}'))
    
    fig.tight_layout()
    fig.set_facecolor('w')
    plt.suptitle("Case-rate by state (rolling 7-day ave.) - " + str_mydate + " \n", fontsize=32, 
                 fontweight=0, color='black', style='oblique')
    plt.xlabel('Source: NY Times COVID-19 Data')
    plt.subplots_adjust(top=0.95)
    
    str_filename = 'case-rate-small-multiples-' + str_mydate + '.png'
    fig.savefig(str_filename);

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
