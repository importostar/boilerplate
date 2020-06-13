---
title: Statistics Analysis
date: 2020-05-07
---
Example Python program Statistics-Analysis.py

## Modules

* from tkinter import *
* from tkinter import ttk
* import tkinter.messagebox
* import matplotlib.pyplot as plt
* import matplotlib.pyplot as plt
* from tkinter import  messagebox
* import numpy as np
* import math
* from statistics import *
* import statistics as sd
* from scipy import stats

## Methods

* def mean2():
* def mode2():
* def median():
* def drow_histogram():
* def drow_boxplot():
* def sd2():
* def personr_and_scatter_drow():

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    import tkinter.messagebox
    import matplotlib.pyplot as plt
    import matplotlib.pyplot as plt
    from tkinter import  messagebox
    import numpy as np
    import math
    from statistics import *
    import statistics as sd
    from scipy import stats
    
    
    
    
    root = Tk()
    root.title('statistical analysis')
    
    root.geometry('300x300+200+200')
    #variables
    mean_mode_median = StringVar()
    
    histo = StringVar()
    
    boxb=StringVar()
    
    person_var1=StringVar()
    person_var2=StringVar()
    #functions
    def mean2():
        s=list(map(int, mean_mode_median.get().split()))
        messagebox.showinfo("the mean is = ",np.mean(s))
    
    def mode2():
        s=list(map(int, mean_mode_median.get().split()))
        messagebox.showinfo("the mode is =",mode(s))
    
    def median():
        s=list(map(int, mean_mode_median.get().split()))
        messagebox.showinfo("the median is = ",np.median(s))
    
    def drow_histogram():
        v=list(map(int, histo.get().split()))
        plt.hist(v)
        plt.show()
    
    def drow_boxplot():
        v=list(map(int, boxb.get().split()))
        plt.boxplot(v)
        plt.show()
    def sd2():
        v=list(map(int, mean_mode_median.get().split()))
        messagebox.showinfo("the Standard devision is = ",sd.stdev(v))
    def personr_and_scatter_drow():
        v1=list(map(int, person_var1.get().split()))
        v2=list(map(int, person_var2.get().split()))
        r,p1=stats.pearsonr(v1, v2)
        messagebox.showinfo("the person r = ",r)
        plt.scatter(v1,v2)
        plt.show()
    
    
    #buttons and text boxs
    boxplot_tx = Entry(root,bg='gray',fg='blue',font='bold 10',textvariable=boxb).pack()
    boxplot_B =ttk.Button(root,text="Box Plot",command=lambda :drow_boxplot()).pack()
    hist_tx = Entry(root,bg='gray',fg='blue',font='bold 10',textvariable=histo)
    hist_tx.pack()
    hist_B = ttk.Button(root,text="Histogram",command=lambda :drow_histogram()).pack()
    mean_median_mode2 = Entry(root,bg='gray',fg='blue',font='bold 10',textvariable=mean_mode_median)
    mean_median_mode2.pack()
    median_B = ttk.Button(root,text="Median",command=lambda :median()).pack()
    mode_B = ttk.Button(root,text="Mode",command=lambda :mode2()).pack()
    mean_B =ttk.Button(root,text="Mean",command=lambda :mean2()).pack()
    sd_B=ttk.Button(root,text="Standard devision",command=lambda :sd2() ).pack()
    rperson1_tx=Entry(root,bg='gray',fg='blue',font='bold 10',textvariable=person_var1).pack()
    rperson2_tx=Entry(root,bg='gray',fg='blue',font='bold 10',textvariable=person_var2).pack()
    rperson_B=ttk.Button(root,text="pearson r and scatter plot",command=lambda :personr_and_scatter_drow()).pack()
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
