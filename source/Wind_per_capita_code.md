---
title: Wind_per_capita_code
date: 2020-05-07
---
Example Python program Wind_per_capita_code.py

## Modules

* from matplotlib import pyplot
* import pandas as pd
* import matplotlib
* import matplotlib.animation as animation

## Methods

* def chart(ctd) :
* def update(*args) :
* def init() :

## Code

Python example

    # -*- coding: utf-8 -*-
    from matplotlib import pyplot
    import pandas as pd
    import matplotlib
    import matplotlib.animation as animation
    
    
    # Database files - Be sure wou change the file's path to where you downloades the files in your machine.
    
    Wind_Consumption = pd.read_csv("C:/Users/Rober/Desktop/CSV/Wind_Consumption.csv",index_col = "Unnamed: 0")
    Wind_Population  = pd.read_csv("C:/Users/Rober/Desktop/CSV/Wind_Population.csv", index_col = "Unnamed: 0")
    
    Year = list(Wind_Consumption)       
    
    pyplot.style.use("seaborn-whitegrid")
    fig, g = pyplot.subplots(figsize=(9.14,5.8))
    pyplot.subplots_adjust(top = 0.915, bottom = 0.075, left = 0.060, right = 0.96)
    pyplot.rcParams['savefig.facecolor'] = "whitesmoke" 
    matplotlib.rcParams['xtick.labelsize'] = 7.0 
    matplotlib.rcParams['ytick.labelsize'] = 7.0 
    
    
    c1 = pyplot.cm.RdYlBu # Colormap
    
    
    def chart(ctd) :
    
       yr = Year[ctd]
      
       y   =  Wind_Consumption[yr]  
       x   =  Wind_Population[yr]/1000000# Converting popolation to million basis.
       lb1 =  list(Wind_Consumption.index)
       lb2 =  Wind_Consumption[yr] * 1000000000 / Wind_Population[yr] # Converting Tw to Kw per capita
       sz  =  Wind_Consumption[yr] * 1000000000 / Wind_Population[yr] * 3 # Bubble size
    
       pyplot.suptitle("Wind Power Consumption Per Capita",fontsize = 11)#, loc = 'center')
       pyplot.title("Top 30 world economies - Data source : British Petroleum and World Bank.",fontsize = 8.0, loc = 'center')
       pyplot.xlabel("Population - Millions",fontsize = 8.0)
       pyplot.ylabel("Consumption - Terawatts hour",fontsize = 8.0)
       pyplot.text(2.9, 320, yr, fontsize = 24, weight = "bold")
       
       cm = 0 
       for p in range(len(x)) : # Scatter plot
           
           labl = lb1[p] + " : " + '{:7.2f}'.format(lb2[p]) # label formatting.
           
           pyplot.scatter(list(x)[p], list(y)[p], s = list(sz)[p], alpha = 0.70, color = c1(cm), marker="o",
                          linewidths = 0.2, edgecolor = "black", label = labl) 
           
           cm+=9
       
    
       fnt = {'fontname':'monospace','weight':'bold'}
       
       if ctd == len(Year)-1 : # Plots the country´s abbreviation (ISO 3 standard).
    
           for l in Wind_Consumption.index :
               
               pyplot.scatter(x[l], y[l], s = 1, alpha = 1, color = "red", marker=".") 
               pyplot.text(x[l], y[l], l, fontsize = 6.8, **fnt)
              
    
      
       pyplot.text(1.08, 590, "In Kw/h Per Capita", fontsize = 6.8, **fnt)
       
       lgnd = pyplot.legend(ncol = 1, loc = "lower left", facecolor = "white",frameon = True, shadow = False,
                            framealpha = 1, prop = {'family':'monospace','size':'6.95','weight':'bold'})
    
     
       # Forces the legend marker's size to be the same - otherwise they would change depending on "s" scatter var. 
       for l in range(0,len(Wind_Consumption)) :
           
           lgnd.legendHandles[l]._sizes = [30]
           
       pyplot.ylim(10**-5,10**3)
       pyplot.yscale("symlog")
       pyplot.xlim(10**0,10**4)
       pyplot.xscale("symlog")
    
       return
    
    
    ctd = 0 # Counter
    fr = len(Year) # Number of frames
    
    def update(*args) :
      
      global ctd
      
      pyplot.clf()
      chart(ctd)
       
      if ctd < fr-1 : # Counter limit
         ctd +=1  
      
      return ()
    
    
    def init() :
      return ()
    
    anim = animation.FuncAnimation(fig, update, init_func=init, blit = False, frames=fr + 13, repeat = False)
    
    sf = "Wind_PerCapita" +".gif"      
    Sname = "C:\\Users\\Rober\Desktop\\_" + sf   # Change to your directory
           
    anim.save(Sname, writer="imagemagick", fps=1)
    
    # You must have imagemagick installed in you computer :
    # https://www.imagemagick.org/script/index.php
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
