---
title: scipy_poly2d_fitting
date: 2020-05-07
---
Example Python program scipy_poly2d_fitting.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import division, print_function
* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.mlab import griddata
* from mpl_toolkits.mplot3d import Axes3D
* from scipy.optimize import curve_fit

## Methods

* def function_poly2d(xy, A, B, C, D, E, F):
* def get_data():
* def poly2d_curve_output(best_params, cov):
* def plotfit_poly2d(x, y, z, fitparam, offset=0.0, title=''):

## Code

Python example

    #!/usr/bin/env python
    from __future__ import division, print_function
    
    import numpy as np
    
    
    def function_poly2d(xy, A, B, C, D, E, F):
        '''
         Return a Second order polynomial function:
         f(x,y) = A * x ** 2  + B * y ** 2 + C * x * y + D * x + E * y + F
         
         INPUT
            xy
                Tuple of numpy arrays containing the x and y coordinates
            A, B, C, D, E, F
                Polinomial coefficients
        '''
        x, y = xy
        return A * x ** 2  + B * y ** 2 + C * x * y + D * x + E * y + F
        
    
    def get_data():
        #Create the coordinates x and y
        x = np.linspace(0, 1024, 40)
        y = np.linspace(0, 2048, 40)
        #Put the coordinates in a mesh
        xx, yy = np.meshgrid(x,y)  
                                                              
        orig_coeff = [0.8, -1.25, 2, 1, -3, 3]
        A, B, C, D, E, F = orig_coeff
        zz = function_poly2d((xx,yy), A, B, C, D, E, F) 
       
        #Flatten the arrays
        xx = xx.flatten()
        yy = yy.flatten()
        #add some noise to zz
        zz = zz.flatten() + np.random.normal(0.0, 200000, len(xx))
        sigma = np.ones(len(xx)) #np.random.rand(len(xx))#
        return xx, yy, zz, sigma
    
        
    def poly2d_curve_output(best_params, cov):
        '''
        Terminal fit output
        '''
        print("=" * 60)
        print('''
                 Least squares fitting with surface:
        A * x ** 2  + B * y ** 2 + C * x * y + D * x + E * y + F
              ''')
        print("=" * 60)
        pars = ['A', 'B', 'C', 'D', 'E', 'F']
        #Diagonal terms of the covariance matrix are the variance of the fitted par   
        error = np.sqrt(np.diagonal(cov))
        print('*'*15 + ' Fitted parameters ' + '*'*15)
        for name, value, sig in zip(pars, best_params, error):
            print("{:s} = {:e} +- {:e}" .format(name, value, sig))
            
        print("Covariance matrix")
        print(cov)
        
            
    def plotfit_poly2d(x, y, z, fitparam, offset=0.0, title=''):
        '''
        Plot the real data and the fitted surface, offsets if required
        '''
        import matplotlib.pyplot as plt
        from matplotlib.mlab import griddata
        from mpl_toolkits.mplot3d import Axes3D
        xi = np.linspace(min(x), max(x))
        yi = np.linspace(min(y), max(y))
        #It is suggested to install the natgrid matplotlib toolkit
        #can be downloaded from 
        #http://sourceforge.net/project/showfiles.php?group_id=80706&package_id=142792
        #For details go to    
        #http://matplotlib.sourceforge.net/api/mlab_api.html#matplotlib.mlab.griddata
        #We grid the data for plotting, using triangulation 
        z_data = griddata(x, y, z, xi, yi)
        xim, yim = np.meshgrid(xi, yi)
        
        A, B, C, D, E, F = fitparam
        z_fit = function_poly2d((xim, yim), A, B, C, D, E, F) + offset
       
        fig = plt.figure()
        
        #plot the surfaces
        ax = Axes3D(fig)
        ax.plot_surface(xim, yim, z_fit, color='red')   
        ax.plot_surface(xim, yim, z_data, color='blue', rstride=5, cstride=5) 
        ax.set_xlabel('x')
        ax.set_ylabel('y')
        ax.set_zlabel('z')
        ax.set_title(title)
        plt.show()  
    
    
    if __name__ == '__main__':
        
        #First you need data. Let's say x, y, z=f(x,y) and stdev
        xx, yy, zz, sigma = get_data()
        
        #Fit     
        from scipy.optimize import curve_fit
        best_par, cov_fit = curve_fit(function_poly2d, (xx,yy), zz, sigma=sigma)
        
        #Print the Output
        poly2d_curve_output(best_par, cov_fit)
        
        #Plot the data and fit (3d plotting)
        plotfit_poly2d(xx, yy, zz, best_par, offset=1000000, title='Least squares method')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
