---
title: sphere_enclosing_points_api
date: 2020-05-07
---
Example Python program sphere_enclosing_points_api.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import mosek 
* import numpy as np
* import plot

## Methods

* def streamprinter(text): 

## Code

Python example

    import sys
    
    import mosek 
    
    import numpy as np
    
    import plot
    
    
    #--------------------------------------------------------
    def streamprinter(text): 
        sys.stdout.write(text) 
        sys.stdout.flush()
    
        
    k=int(sys.argv[1]) #number of points
    n=int(sys.argv[2]) #dimension
    
    p=  np.random.normal(size=(k,n))
    
    env = mosek.Env()
    task= env.Task(0,0)
    
    numvar= 1 + n + k*n + k
    
    offset_r= 0
    offset_p= 1
    offset_w= 1+n
    offset_t= 1+n+n*k
    
    task.appendvars(numvar)
    task.putvarboundslice(0,numvar,[mosek.boundkey.fr for i in range(numvar)], np.zeros(numvar), np.zeros(numvar))
    
    
    numcon= 2*k + k
    task.appendcons(numcon)
    
    for i in range(k):#for each point
        task.putarow(i, [0,i+offset_t], [1., -1,]) #delta coord#radius aux
        task.putconbound(i, mosek.boundkey.fx, 0. ,0.)
    
        for j in range(n):
            task.putconbound(k+ i*n + j, mosek.boundkey.fx, p[i][j] , p[i][j])
            task.putarow(k+i*n + j,[offset_p + j, offset_w+i*n + j],[1.0,-1.0])
    
        task.appendcone(mosek.conetype.quad,0., np.hstack([ offset_t+i, [ offset_w+i*n + j for j in range(n)]] ))
            
    task.putcj(0,1.0)
    task.putobjsense(mosek.objsense.minimize)
    
    task.set_Stream (mosek.streamtype.log, streamprinter)
    task.writedata("dump.opf")
    
    task.optimize()
    
    xx = np.zeros(numvar, float) 
    task.getxx(mosek.soltype.itr,xx)
    
    r0= xx[0]
    p0= xx[1:n+1]
    
    print(r0,p0)
    
    
    #comment out this block if you haven't matplotlib installed
    if n==2:
        plot.plot_points(p,p0,r0)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
