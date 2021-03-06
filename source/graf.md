---
title: graf
date: 2020-05-07
---
Example Python program graf.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pandas as pd
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.colors as col
* from matplotlib import rc # this is the matplotlib suggestion

## Code

Python example

    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    import pandas as pd
    import matplotlib
    import matplotlib.pyplot as plt
    import matplotlib.colors as col
    from matplotlib import rc # this is the matplotlib suggestion
    
    pd.set_option('float_format', '{:f}'.format)
    
    matplotlib.rc('font', family='DejaVu Sans')
    
    path = "D:\\CTU\\Zimni semestr 2017\\PycharmProjects\\preprocessing\\Hadoop_OUTPUTS_for_CHARTS\\CALLs_repeating_percent\\000000_0"
    
    a= pd.read_csv(path,sep=",",names=["cf","ct","pocet_pakovani","pr"])
    
    
    A_df = a[["cf"]]
    B_df = a[["ct"]]
    C_df = a.apply(lambda x:'%s -> %s' % (x["cf"],x['ct']),axis=1)
    print(C_df)
    #C_df = a.apply(lambda x:"{0}xx{1} -> {2}xx{3}".format(x["cf"][:3], x["cf"][9:],x["ct"][:3], x["ct"][9:]),axis=1)
    
    
    #a.plot(x= C_df, y='op',style='o')
    a.plot(x=C_df, y='pocet_pakovani',style='o',kind = "barh")
    plt.ylabel(u'volající, volaný [-,-]')
    plt.xlabel(u'počet opakových hovorů [-]')
    plt.title(u"Diagram opakujících se hovorů")
    plt.setp( plt.gca().get_xticklabels(),rotation= 20,horizontalalignment = 'right')
    plt.subplots_adjust(left  = 0.22, right = 0.90, bottom = 0.11,top = 0.88,wspace = 0.20,hspace = 0.20)
    #plt.savefig("graf.png")
    plt.show()
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
