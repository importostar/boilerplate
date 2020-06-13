---
title: li_re
date: 2020-05-07
---
Example Python program li_re.py

## Modules

* import matplotlib
* import numpy as np
* import matplotlib.cm as cm
* import matplotlib.mlab as mlab
* import matplotlib.pyplot as plt

## Methods

* def cost(t0,t1):
* def cost_del_t0(t0,t1):
* def cost_del_t1(t0,t1):
* def gra_de1(alpha, times, inicial0, inicial1):
* def gra_de2(alpha, times, inicial0, inicial1):
* def hypothesis1(x):
* def hypothesis2(x):

## Code

Python example

    import matplotlib
    import numpy as np
    import matplotlib.cm as cm
    import matplotlib.mlab as mlab
    import matplotlib.pyplot as plt
    
    %matplotlib inline
    
    
    features = np.array([0.8,0.9,1.0,1.1,1.4,\
    	1.4,1.5,1.6,1.8,2.0,2.4,2.5,2.7,3.2,3.5])
    target = np.array([70,83,74,93,89,58,85,114,95,100,138,111,124,161,172])
    
    plt.plot(features,target,'o', markersize=10)
    plt.show()
    
    def cost(t0,t1):
        return (np.sum(((features*t1 +t0)- target)**2))/(2*len(features))
    
    def cost_del_t0(t0,t1):
        return np.sum(((features*t1 +t0)- target))/len(features)
    
    def cost_del_t1(t0,t1):
        return np.sum((features*t0) + (features**2)*t1\
         - features*target)/len(features)
      
    
    #gradient Descent fixed alpha       
    def gra_de1(alpha, times, inicial0, inicial1):
        i0 = inicial0
        i1 = inicial1
        for i in range(times):
            temp0 = i0 - alpha*cost_del_t0(i0,i1) 
            temp1 = i1 - alpha*cost_del_t1(i0,i1)
            i0 = temp0
            i1 = temp1
        return i0,i1
    
    
    
    #gradient Descent decreasing alpha     
    def gra_de2(alpha, times, inicial0, inicial1):
        i0 = inicial0
        i1 = inicial1
        for i in range(times):
            alpha = alpha - alpha*(i/(times-1))
            temp0 = i0 - alpha*cost_del_t0(i0,i1) 
            temp1 = i1 - alpha*cost_del_t1(i0,i1)
            i0 = temp0
            i1 = temp1
        return i0,i1
    
    
    test1 = gra_de1(0.3, 500,0,0)
    
    test2 = gra_de2(0.6, 500,0,0)
    
    def hypothesis1(x):
        return test1[0] + test1[1]*x
    
    def hypothesis2(x):
        return test2[0] + test2[1]*x
    
    plt.plot(features, hypothesis1(features),\
    	features,hypothesis2(features),features,target,'o', markersize=10)
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
