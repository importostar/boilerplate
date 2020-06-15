---
title: 05_local_contrast_norm
date: 2020-05-07
---
Example Python program 05_local_contrast_norm.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import math, sys
* import mahotas as mh
* import scipy.stats as st

## Methods

* def draw_image(data, size):
* def norm_filter(size, sigma=1):
* def add_padding_center(data, filter_size):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import numpy as np
    import math, sys
    import mahotas as mh
    import scipy.stats as st
    
    plt.style.use('fivethirtyeight')
    
    def draw_image(data, size):
        Z = data.reshape(size,size)   # convert from vector to 28x28 matrix
        Z = np.array(Z[::-1,:])       # flip vertical
        plt.pcolor(Z)
        plt.gray()
        plt.tick_params(labelbottom="off")
        plt.tick_params(labelleft="off")
    
    def norm_filter(size, sigma=1):
        r= math.floor(size/2)
        if (size %2) != 0:
            pad = 0
        else:
            pad = 1
        x = np.linspace(-r+pad,r, size)
        y = np.linspace(-r+pad,r, size)
        X, Y = np.meshgrid(x, y)
        
        Z = st.multivariate_normal.pdf(np.dstack((X,Y)), mean=[0,0], cov=[[sigma,0],[0,sigma]])
        plus = (1. - np.sum(Z)) / float(size*size)
        return Z + plus
    
    def add_padding_center(data, filter_size):
        if type(data) != np.ndarray:
            raise Exception('data must be numpy.ndarray')  
            
        if (filter_size %2) != 0:
            # odd
            pad_size = (filter_size-1)/2
        else:
            #even
            pad_size = filter_size/2
    
        return np.lib.pad(data, ((pad_size,pad_size),(pad_size,pad_size)), 'edge')
    
    # prepare filter
    filter_size = 17
    plt.figure(figsize=(7,7))
    draw_image(padded_lenna.flatten(), im_lenna.shape[0] + filter_size-1)
    norm_f = norm_filter(filter_size, sigma=15)
    plt.figure(figsize=(5,5))
    draw_image(norm_f.flatten(), filter_size)
    
    # prepare Lenna image
    im = mh.imread('./lenna-ring.jpg', as_grey=True)
    im_size = im.shape[0]
    im_lenna = im.astype(np.float32)
    im_lenna = (im_lenna-np.min(im_lenna)) / float(np.max(im_lenna)-np.min(im_lenna))
    padded_lenna = add_padding_center(im_lenna, filter_size)
    
    # forで回しすぎて怒られそうなコードだ・・・
    for i in range(im_size):
        sys.stdout.write("i:{}".format(i))
        for j in range(im_size):
            im_lenna[i,j] -= np.sum([padded_lenna[i+p, j+q] * norm_f[p, q] \
                                     for p in range(filter_size) for q in range(filter_size)])
            
    plt.figure(figsize=(7,7))
    draw_image(im_lenna.flatten(), im_size)
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
