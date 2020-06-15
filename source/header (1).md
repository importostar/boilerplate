---
title: header (1)
date: 2020-05-07
---
Example Python program header (1).py

## Modules

* from IPython.core.display import display, HTML
* from IPython.core.interactiveshell import InteractiveShell
* display(HTML("<style>.container { width:95% !important; }</style>"))
* import matplotlib
* import matplotlib.pyplot as plt
* import pandas as pd
* import seaborn as sns
* import numpy as np
* from tqdm.auto import tqdm

## Code

Python example

    %load_ext autoreload
    %autoreload 2
    
    %matplotlib inline
    %config InlineBackend.figure_format = 'retina'
    
    from IPython.core.display import display, HTML
    from IPython.core.interactiveshell import InteractiveShell
    InteractiveShell.ast_node_interactivity = "all"
    
    display(HTML("<style>.container { width:95% !important; }</style>"))
    
    import matplotlib
    import matplotlib.pyplot as plt
    import pandas as pd
    import seaborn as sns
    import numpy as np
    from tqdm.auto import tqdm
    
    sns.set_style("ticks")
    
    # Japanese font installation
    # 1) `$ mkdir $HOME/.fonts`
    # 2) Download Osaka.ttf tp $HOME/.fonts/
    # 3) `$ fc-cache`
    # 4) (optional) Clear matplotlib cache dir, find the dir with `matplotlib.get_cachedir()`
    plt.rcParams['font.family'] = 'Osaka'
    
    pd.set_option('display.max_rows', 500)
    pd.set_option('display.max_columns', 500)
    pd.set_option('display.width', 1000)
    pd.set_option('display.max_colwidth', 500)
    pd.set_option('display.float_format', lambda x: '%.3f' % x)
    
    np.set_printoptions(suppress=True)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
