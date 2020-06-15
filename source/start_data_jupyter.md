---
title: start_data_jupyter
date: 2020-05-07
---
Example Python program start_data_jupyter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import json
* import numpy as np
* import matplotlib.pyplot as plt
* import pandas as pd
* import os
* from pyspark import SparkContext, SparkConf
* import json
* import numpy as np
* import os
* import json
* import numpy as np
* import matplotlib.pyplot as plt
* import pandas as pd
* import seaborn as sns

## Code

Python example

    #############
    # BASE CONFIG
    #############
    
    %load_ext autoreload
    %autoreload 2
    %matplotlib inline
    
    
    import os
    import json
    import numpy as np
    import matplotlib.pyplot as plt
    import pandas as pd
    
    BASE_DATA_DIR = './data'
    
    #############
    # SPARK CONFIG
    #############
    
    %load_ext autoreload
    %autoreload 2
    %matplotlib inline
    
    import os
    from pyspark import SparkContext, SparkConf
    import json
    import numpy as np
    
    config = SparkConf().setAll([('spark.executor.memory', '8g'), 
                                 ('spark.executor.cores', '3'), 
                                 ('spark.cores.max', '3'), 
                                 ('spark.driver.memory','8g')])
    sc = SparkContext(conf=config)
    print("SPARK CONFIG: ", sc.getConf().getAll())
    
    #############
    # SEABORN CONFIG
    #############
    
    %load_ext autoreload
    %autoreload 2
    %matplotlib inline
    
    
    import os
    import json
    import numpy as np
    import matplotlib.pyplot as plt
    import pandas as pd
    import seaborn as sns
    sns.set_style("whitegrid")
    plt.figure(num=None, figsize=(8, 6), dpi=80, facecolor='w', edgecolor='k')
    
    BASE_DATA_DIR = './data'
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
