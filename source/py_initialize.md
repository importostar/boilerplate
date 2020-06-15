---
title: py_initialize
date: 2020-05-07
---
Example Python program py_initialize.py

## Modules

* # import modules and establish Oracle ODBC connection
* import matplotlib.pyplot as plt  
* import matplotlib.colors as colors
* import matplotlib.cm as cm
* import pyodbc
* import pandas as pd
* import numpy as np
* from IPython.display import display
* import datetime
* import json
* from matplotlib.font_manager import FontProperties

## Code

Python example

    # import modules and establish Oracle ODBC connection
    
    # plot config
    import matplotlib.pyplot as plt          
    import matplotlib.colors as colors
    import matplotlib.cm as cm
    
    
    %matplotlib inline
    import pyodbc
    import pandas as pd
    import numpy as np
    from IPython.display import display
    import datetime
    import json
    
    
    config = json.loads(open(r"""C:\tools\config.json""").read())
    
    cnxn = pyodbc.connect('DSN=PROD;PWD=' + config['Oracle_pwd'])
    
    cursor = cnxn.cursor()
    
    plt.style.use('fivethirtyeight')
    
    from matplotlib.font_manager import FontProperties
    
    font0 = FontProperties()
    font1 = font0.copy()
    font1.set_size('large')
    family = ['serif', 'sans-serif', 'cursive', 'fantasy', 'monospace']
    font = font0.copy()
    font.set_family(family[1])
    font.set_name('Bariol')
    font.set_size(10)
    
    STD_COLORS = {
              'khg':     '#00A8EC',
              '1':       '#e41a1c',
              '2':       '#377eb8',
              '3':       '#4daf4a',
              '4':       '#984ea3',
              '5':       '#ff7f00',
              '6':       '#ffff33',
              '7':       '#1b9e77',
              '8':       '#d95f02',
              '9':       '#7570b3'}

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
