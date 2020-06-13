---
title: ecg_chart
date: 2020-05-07
---
Example Python program ecg_chart.py

## Modules

* import matplotlib
* from matplotlib.backends.backend_pdf import PdfPages
* import matplotlib.pyplot as plt

## Methods

* def get_line_width(i):

## Code

Python example

    #*-- coding: utf-8 --*
    
    import matplotlib
    
    X_INCH = 7
    Y_INCH = 11
    X_MM = int(X_INCH*25.4)
    Y_MM = int(Y_INCH*25.4)
    
    while X_MM % 5 != 1:
        X_MM -= 1
    
    while Y_MM % 5 != 1:
        Y_MM -= 1
    
    M_X_INCH = float(X_MM) / 25.4
    M_Y_INCH = float(Y_MM) / 25.4
    THIN_WIDTH = 0.2
    FAT_WIDTH = 0.6
    
    
    matplotlib.use('pdf')
    from matplotlib.backends.backend_pdf import PdfPages
    
    import matplotlib.pyplot as plt
    
    with PdfPages('ecg.pdf') as pdf:
    
        f = plt.figure(figsize=(M_X_INCH,M_Y_INCH), dpi=600)  # 英寸
        plt.rc('lines', linewidth=THIN_WIDTH, color='hotpink')
        # 坐标系
        # axes = f.add_subplot(1,1,1)
        axes = f.add_axes( (0, 0, 1, 1), frame_on=False )
        axes.set_xlim(-0.5, X_MM-0.5)     # 毫米
        axes.set_ylim(-0.5, Y_MM-0.5)    
        def get_line_width(i):
            if i % 5 == 0 :
                return FAT_WIDTH 
            else:
                return THIN_WIDTH
        for i in range(0, X_MM):
            axes.axvline(x=i,linewidth=get_line_width(i))
        for i in range(0, Y_MM):
            axes.axhline(y=i,linewidth=get_line_width(i))
    
        pdf.savefig()
        plt.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
