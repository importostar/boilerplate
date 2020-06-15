---
title: 04_anim_Lp_pooling_beta
date: 2020-05-07
---
Example Python program 04_anim_Lp_pooling_beta.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import scipy.stats as st

## Methods

* def animate(nframe):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import numpy as np
    import scipy.stats as st
    
    plt.style.use('ggplot')
     
    np.random.seed(0)
    x_max = 1000
    num = x_max * 100
    # caluculation takes a certain time due to using float128
    P = np.linspace(1,x_max,num).astype(np.float128)
    h_range = xrange(1, 16)
    
    # Beta Random Variable
    a=1.5
    b=20
    z = np.array([st.beta.rvs(a, b, loc=0, scale=1, size=500)*h for h in h_range])
        
    Lp_list = []
    for h in h_range:
        zz = z[h-1].astype(np.float128)
        H = float(len(zz))
        Lp_list.append([((1/H)*np.sum(zz**p))**(1/p) for p in P])
        
    def animate(nframe):
        sys.stdout.write("{}, ".format(nframe))
        plt.clf()
        zmax = np.max(z[nframe])
        col = "bgrcmyk"*3
        plt.style.use('ggplot')
        plt.subplot(2,1,1)
        Lp = Lp_list[nframe]
        plt.ylim(0,6)
        plt.xlim(0,500)
        plt.xlabel("P")
        plt.ylabel("Lp")
        plt.title("Lp pooling plot with changing P, max={0:.3f}".format(zmax))
        plt.plot([0,500],[zmax,zmax],"k--")
        plt.plot(P[:50000], Lp[:50000], c=col[nframe])
        
        plt.subplot(2,1,2)
        plt.ylim(0,6)
        plt.title("Beta({2},{3}) random variable, min=0, max={0:.3f}, ave={1:.3f}".format(zmax,np.mean(z[nframe]),a,b))
        plt.plot([0,500],[zmax,zmax],"k--")
        plt.plot(z[nframe], c=col[nframe])
        
    fig = plt.figure(figsize=(10,10))
    
    anim = ani.FuncAnimation(fig, animate, frames=len(Lp_list), blit=True)
    anim.save('anim_beta_Lp.gif', writer='imagemagick', fps=2, dpi=64)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
