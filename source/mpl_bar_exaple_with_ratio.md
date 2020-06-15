---
title: mpl_bar_exaple_with_ratio
date: 2020-05-07
---
Example Python program mpl_bar_exaple_with_ratio.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import pandas as pd
* import seaborn as sns

## Code

Python example

    """Example of matplotlib barplot with accumulative ratio on 2nd axis."""
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas as pd
    import seaborn as sns
    
    # Plot with seaborn darkgrid style
    % matplotlib inline
    sns.set(style="darkgrid", palette="muted", color_codes=True)
    
    # Generate toy data
    df = pd.DataFrame({'group': ['A', 'B', 'C', 'D', 'E'],
                       'value': [20, 30, 10, 50, 40]})
    
    # Genarate x coorinate point
    # matplotlib Barplot require x-coordinate to point
    x_idx = np.arange(df.shape[0])
    
    # Get fig and ax to plot within
    fig, ax = plt.subplots()
    
    # Add barplot(1st axis)
    bar = ax.bar(left=x_idx,
                 height=df['value'],
                 tick_label=df['group'],
                 alpha=0.7
                 )
    
    # Add x/y label to 1st axis
    ax.set_xlabel('Group')
    ax.set_ylabel('Value[]')
    
    # Add annotation to 1st axis
    margin = 1
    for x, y in zip(x_idx, df['value']):
        ax.text(x, y + margin, y, color='b')
    
    # Calc accumulative ratio as secondaly axis value
    df['accumulative_ratio'] = df['value'].cumsum() / df['value'].sum()
    
    # Plot lines with secondaly axis
    ax2 = ax.twinx()
    line = ax2.plot(x_idx,
                    df['accumulative_ratio'],
                    ls='--',
                    marker='o',
                    color='r'
                    )
    
    # Add x/y label to 1st axis
    ax2.set_ylabel('Accumulaive ratio[]')
    ax2.grid(visible=False)
    
    # Add annotation to 2nd axis
    margin = 0.08
    for x, y in zip(x_idx, df['accumulative_ratio']):
        ax2.text(x, y + margin, '{:.1f}'.format(y), color='r')
    
    plt.legend(handles=(bar[0], line[0]),
               labels=('Value', 'Accumulaive_ratio'))
    
    plt.suptitle('Example of barplot with secondaly axis.')
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
