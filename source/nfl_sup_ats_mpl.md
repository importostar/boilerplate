---
title: nfl_sup_ats_mpl
date: 2020-05-07
---
Example Python program nfl_sup_ats_mpl.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import csv, os
* import numpy as np
* import pandas as pd
* from datetime import datetime
* import matplotlib.pyplot as plt
* import matplotlib

## Code

Python example

    import csv, os
    import numpy as np
    import pandas as pd
    # print pd.__version__
    
    from datetime import datetime
    
    import matplotlib.pyplot as plt
    import matplotlib
    matplotlib.style.use('ggplot')
    %matplotlib inline
    
    home_lines = pd.read_csv('data/ATS_SUP_home_conf.csv', sep=';')
    print home_lines.shape
    print home_lines.dtypes
    print ''
    print home_lines.head()    # only first 3 weeks of season at this point
    
    # (48, 9)
    # week                object
    # away_short_name     object
    # home_short_name     object
    # away_score           int64
    # home_score           int64
    # home_line          float64
    # home_conf           object
    # home_favBy         float64
    # home_ptd             int64
    # dtype: object
    
    #      week away_short_name home_short_name  away_score  home_score  home_line  \
    # 0  Week 1             CAR             DEN          20          21        3.5   
    # 1  Week 1             BUF             BAL           7          13       -3.5   
    # 2  Week 1             CHI             HOU          14          23       -6.5   
    # 3  Week 1             CIN             NYJ          23          22        2.5   
    # 4  Week 1             CLE             PHI          10          29       -3.5   
    
    #   home_conf  home_favBy  home_ptd  
    # 0       AFC        -3.5         1  
    # 1       AFC         3.5         6  
    # 2       AFC         6.5         9  
    # 3       AFC        -2.5        -1  
    # 4       NFC         3.5        19 
    
    
    home_lines['abs_line_ptd'] = np.absolute(home_lines.home_favBy - home_lines.home_ptd)
    
    ### now, the plot
    
    # # not a perfect way of making smaller points visible // get over it
    s_afc = (home_lines[home_lines.home_conf=='AFC']['abs_line_ptd'] + 1)*10
    s_nfc = (home_lines[home_lines.home_conf=='NFC']['abs_line_ptd'] + 1)*10
    
    ax = home_lines[home_lines.home_conf=='AFC']\
            .plot.scatter(x='home_favBy', 
                          y='home_ptd', color='red',
                          s=s_afc,
                          alpha=0.5,
                          label='AFC',
                          figsize=(8,8)
                         )
        
    home_lines[home_lines.home_conf=='NFC']\
            .plot.scatter(x='home_favBy', 
                          y='home_ptd', color='blue',
                          s=s_nfc,
                          alpha=0.5,
                          label='NFC', ax=ax
                         )
    
    ats = np.linspace(-35,35,100)
    fav = np.linspace(-35,35,100)
    ptd = np.linspace(-35,35,100)
    
    plt.plot(ats, ats, 'g--')
    plt.plot(fav, np.zeros(100), 'k-')
    plt.plot(np.zeros(100), ptd, 'k-')
    plt.xlim([-35,35])
    plt.ylim([-35,35])
    
    plt.title("2016 Home Performance SUP & ATS\n(through week 3)")
    plt.xlabel("Home Team Favored By", fontweight='bold')
    plt.ylabel("Home Point Difference", fontweight='bold')
    
    plt.legend(bbox_to_anchor=(0, 1), loc='lower right', ncol=1)
    
    plt.text(25, 1, 'Win SUP', fontsize=10, fontweight='bold', color='darkblue')
    plt.text(25, -2.5, 'Lose SUP', fontsize=10, fontweight='bold', color='dodgerblue')
    
    plt.text(25, 32, 'Win ATS', fontsize=10, fontweight='bold', rotation=45)
    plt.text(27.5, 30.5, 'Lose ATS', fontsize=10, fontweight='bold', color='red', rotation=45)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
