---
title: twitter
date: 2020-05-07
---
Example Python program twitter.py

## Modules

* import csv
* import matplotlib
* import matplotlib.pyplot as plt
* import pandas as pd
* import os
* import sys
* from pandas.plotting import register_matplotlib_converters

## Code

Python example

     
    import csv
    import matplotlib
    import matplotlib.pyplot as plt
    import pandas as pd
    import os
    import sys
    from pandas.plotting import register_matplotlib_converters
    
    register_matplotlib_converters()
    
    tweet_id, in_reply_to_status_id, in_reply_to_user_id, timestamp, source, text, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp, expanded_urls = range(10)
    
    match = sys.argv[1]
    
    csv_reader = csv.reader(sys.stdin, delimiter=',')
    date_list, coincidences_list = [], []
    for tweet in csv_reader:
        if not tweet[retweeted_status_id]:
            date_list.append(tweet[timestamp][:19])
            tweet[text] = tweet[text].replace(os.linesep, ' ')
            coincidences_list.append(1 if match in tweet[text]else 0)
    
    df = pd.DataFrame()
    df['datetime'] = pd.to_datetime(date_list)
    df.index = df['datetime'] 
    df['coincidences'] = coincidences_list
    df_sampled = df.resample('D').sum()
    
    fig, ax = plt.subplots()
    ax.plot(df_sampled.index, df_sampled['coincidences'])
    ax.set(xlabel='date', ylabel='coincidences', title=match+' from:socialimscr')
    ax.grid()
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
