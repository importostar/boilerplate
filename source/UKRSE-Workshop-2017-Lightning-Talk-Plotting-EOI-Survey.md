---
title: UKRSE Workshop 2017 Lightning Talk Plotting EOI Survey
date: 2020-05-07
---
Example Python program UKRSE-Workshop-2017-Lightning-Talk-Plotting-EOI-Survey.py

## Modules

* import seaborn as sns
* import pandas as pd
* import warnings
* import matplotlib.pyplot as plt;
* import matplotlib;
*   'Increased recognition for the importance of the RSE role': 'Recognition for RSEs',

## Code

Python example

    import seaborn as sns
    import pandas as pd
    import warnings
    import matplotlib.pyplot as plt;
    import matplotlib;
    matplotlib.style.use('ggplot');
    
    txtfile='RSE-EOI-survey-list-anonymized-v2.csv'
    
    rse_df = pd.read_csv(txtfile,
                         delimiter=',',
                         index_col=False)
    rse_df['Degree'].fillna(rse_df.OtherDegree, inplace=True)
    rse_df['Priority'].fillna(value='Other', inplace=True)
    del rse_df['OtherDegree']
    del rse_df['OtherPriority']
    
    %matplotlib inline
    figsize=(8,8);
    fontsize=32;
    plt.figure(figsize=figsize);
    
    rse_df.Degree.unique()
    rse_df.Degree.value_counts()
    
    pd.value_counts(rse_df['Degree'])
    
    pd.value_counts(rse_df['Degree']).plot(kind='pie',autopct='%0.1f', figsize=figsize, fontsize=fontsize);
    
    replace_values = {'More long-term career options within research community': 'Long-term career pathways in research',
                      'Increased opportunities to meet and interact with other RSEs': 'Interactions with other RSEs',
                      'Increased recognition for the importance of the RSE role': 'Recognition for RSEs',
                      'Sharing of best practices and new technologies with other RSEs': 'Sharing best-practices'}
    rse_df['Priority'].replace(replace_values, inplace=True)
    
    matplotlib.rcParams['text.usetex'] = False
    pd.value_counts(rse_df['Priority']).plot(kind='pie',label='', figsize=figsize,colormap='Set2', autopct='%0.1f',fontsize=fontsize);
    
    pri = sns.countplot(y="Priority", hue="Degree", data=rse_df, palette='muted')
    plt.legend(loc='lower right');
    pri.figure.set_size_inches(figsize)
    ax = pri.axes
    for item in ([ax.title, ax.xaxis.label, ax.yaxis.label] +
                 ax.get_xticklabels() + ax.get_yticklabels()):
        item.set_fontsize(fontsize)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
