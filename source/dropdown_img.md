---
title: dropdown_img
date: 2020-05-07
---
Example Python program dropdown_img.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from ipywidgets import interact,Dropdown
* from scipy import ndimage
* import ipywidgets
* import matplotlib
* import scipy

## Methods

* def f(im_dd):

## Code

Python example

    %matplotlib widget
    import numpy as np
    import matplotlib.pyplot as plt
    from ipywidgets import interact,Dropdown
    from scipy import ndimage
    plt.rcParams['font.size']=12
    plt.rcParams['font.family'] = 'sans-serif'
    
    #make data
    im_list=[]
    for i in [3,4,5]:
        n = i
        s = 128
        im = np.zeros((s, s))
        points = (s*np.random.random((2, n**2))).astype(int)
        im[points[0], points[1]] = 10000
        im = ndimage.gaussian_filter(im, sigma=s/(8.*n))
        im_list.append(im)
        
    #show
    fig, ax = plt.subplots(figsize=(4,4))
    img = [ax.imshow(im_list[0], cmap=plt.cm.gist_earth)]
    
    im_dd = Dropdown(
        options=[('image1', 0), ('image2', 1), ('image3', 2)],
        value=0,
        description='Select image:')
    @interact(im_dd=im_dd)
    def f(im_dd):    
        ax.cla()
        ax.imshow(im_list[im_dd], cmap=plt.cm.gist_earth)
     
    
    #version
    import ipywidgets
    print(ipywidgets.__version__)
    #7.5.1
    
    import matplotlib
    print(matplotlib.__version__)
    #3.2.0
    
    print(np.__version__)
    #1.18.1
    
    import scipy
    print(scipy.__version__)
    #1.4.1

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
