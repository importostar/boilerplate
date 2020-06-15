---
title: HW
date: 2020-05-07
---
Example Python program HW.py

## Modules

* import matplotlib.pyplot as plt
* from sympy import *

## Methods

* def p(x):

## Code

Python example

    import matplotlib.pyplot as plt
    from sympy import *
    
    x = symbols("x")
    f = sin(x)
    f_fun = lambdify(x, f)
    x0 = 0
    n = 2
    
    coeffs = []
    for i in range(n):
            f = diff(f, "x")
            coeffs.append(f.evalf(subs = {x: x0}))
            
    def p(x):
        result = f_fun(x0)
        current_coeff = 1
        for i in range(n):
            current_coeff *= (x - x0) / (i+1)
            result += coeffs[i]*current_coeff
            
        return
        
    a, b = -8, 8
    N = 100
    x_list = [a +i*(b-a)/(N-1) for i in range(N)]
    y1_list = list(map(f_fun, x_list))
    y2_list = list(map(p, x_list))
    
    plt.axis("equal")
    plt.plot(x_list, y1_list)
    plt.plot(x_list, y2_list)
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
