---
title: data_visualization
date: 2020-05-07
---
Example Python program data_visualization.py

## Modules

* import matplotlib.pyplot as plt
* import matplotlib
* import seaborn as sns

## Code

Python example

    ## many plot package are matplotlib-based
    
    ## it's good to start with solving issues in matplotlib!
    import matplotlib.pyplot as plt
    
    
    ##### avoid redundant blank or cutting-off
    
    plt.savefig("test.png", bbox_inches='tight')
    
    
    ##### avoid overlapping when using matplotlib savefig  
    
    ## to clear buffer
    plt.clf()
    
    ##### avoid error when running .py file in shell
    
    import matplotlib
    matplotlib.use('Agg')
    
    
    ##### use for loop to create subplots 
    
    fig = plt.figure(figsize=(20, 10))
    for i in range(total_num):
        ax = plt.subplot(4, total_num/4, i+1)
        plt.plot([1,2,3,4,5])
    fig.tight_layout()
    
    ##### hide x y ticks
    
    plt.xticks([], [])
    plt.yticks([], [])
    
    
    
    ##### percentage barplot
    
    import seaborn as sns
    df = sns.load_dataset("tips")
    props = df.groupby("day")['sex'].value_counts(normalize=True).unstack()
    props.plot(kind='bar', stacked='True')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
