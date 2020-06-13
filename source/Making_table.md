---
title: Making_table
date: 2020-05-07
---
Example Python program Making_table.py

## Modules

* import numpy as np
* import sys
* #import jsonschema
* #import yaml
* import pandas as pd
* import matplotlib
* import matplotlib.pyplot as plt

## Methods

* def ReadSummary_trm(smry):
* def ReadSummary_map(smry):
* def plot_matrix(df,out):

## Code

Python example

    #!/usr/bin/env python3
    # coding: utf-8
    import numpy as np
    import sys
    #import jsonschema
    #import yaml
    import pandas as pd
    import matplotlib
    matplotlib.use('Agg')
    import matplotlib.pyplot as plt
    #pip install matplotlib --upgrade --ignore-installed six
    
    
    def ReadSummary_trm(smry):
        d_ = pd.read_csv(smry,delimiter='\t',index_col=0,skiprows=[1,2,5,6,7,8,9],header=None)
        #d_[1][1:].astype(int)*2
        d_ = d_.T
        d_ = d_.rename(columns={'State':'Sample_Name'}) 
        return d_
    
    def ReadSummary_map(smry):
        d_ = pd.read_csv(smry,delimiter='\t',index_col=0,skiprows=[1,2,3,6,7,8],header=None)
        d_ = d_.T
        d_ = d_.rename(columns={'State':'Sample_Name'}) 
        return d_
    
    def plot_matrix(df,out):
        fig,ax = plt.subplots(figsize=(len(df.columns)*4, len(df.index)*1.0))
        #print (df['Sample_Name'])
        tbl = ax.table(cellText=df.values,bbox=[0,0,1,1],colLabels=df.columns,loc='center')
        tbl.auto_set_font_size(False)
        tbl.set_fontsize(len(df.columns)*4)
        ax.axis('off')
        cellDict=tbl.get_celld()
        for c in range(0,len(df.columns)):
               cellDict[(0,c)].set_facecolor('#dbdbdc')
               #cellDict[(0,c)].set_width(1.5)
        plt.savefig(out)
    
    if __name__ == '__main__':
        smry = "./RNA-seq_Summary.txt"
        d__ = ReadSummary_trm(smry)
        plot_matrix(d__,"./test.png")
        d__2 = ReadSummary_map(smry)
        plot_matrix(d__2,"./test2.png")
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
