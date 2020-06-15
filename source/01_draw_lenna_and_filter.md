---
title: 01_draw_lenna_and_filter
date: 2020-05-07
---
Example Python program 01_draw_lenna_and_filter.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import math
* import mahotas as mh
* import os.path

## Methods

* def draw_image(data, size):
* def gen_cos_filter(size, theta=0, freq=1, phase=0):
* def add_padding_0(data, pad_length):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import numpy as np
    import math
    import mahotas as mh
    import os.path
    
    # get Lenna image
    if os.path.isfile('./lenna.jpg'):
        im = mh.demos.load('lena')
        mh.imsave('lenna.jpg', im)
    
    plt.style.use('fivethirtyeight')
    
    def draw_image(data, size):
        Z = data.reshape(size,size)   # convert from vector to 28x28 matrix
        Z = np.array(Z[::-1,:])       # flip vertical
        plt.pcolor(Z)
        plt.gray()
        plt.tick_params(labelbottom="off")
        plt.tick_params(labelleft="off")
    
    def gen_cos_filter(size, theta=0, freq=1, phase=0):
        if (size %2) != 0:
            tuning = 0.5
        else:
            tuning = 0
    
        _min = size - math.floor(size/2) - tuning
        _max = size + math.floor(size/2) + tuning
        
        xx = np.linspace(_min, _max, size)
        yy = np.linspace(_min, _max, size)
        X, Y = np.meshgrid(xx, yy)
    
        # Rotation 
        x_theta =  (X*freq+phase)*np.cos(theta) + (Y*freq+phase)*np.sin(theta)
        ret = np.cos(x_theta)
        return np.array(ret)*2
    
    def add_padding_0(data, pad_length):
        if type(data) != np.ndarray:
            raise Exception('data must be numpy.ndarray')
        return np.lib.pad(data, ((0, pad_length), (0, pad_length)), 'constant', constant_values=0)
    
    im = mh.imread('./lenna.jpg', as_grey=True)
    im_size = im.shape[0]
    im_lenna = im.astype(np.float32)
    im_lenna = (im_lenna-np.min(im_lenna)) / float(np.max(im_lenna)-np.min(im_lenna))
    im_lenna = add_padding_0(im_lenna, 16)
    
    plt.figure(figsize=(7,7))
    
    filter_size = 17
    plt.figure(figsize=(3,3))
    
    filter_type = 1
    
    if filter_type == 0:
        #
        sin_filter = gen_cos_filter(filter_size, theta=np.pi/4, freq=.346, phase=-1.5)
    else:
        #
        sin_filter = gen_cos_filter(filter_size, theta=-np.pi/4, freq=.646, phase=-1.5)
        
    
    draw_image(sin_filter, filter_size)
    sin_filter = sin_filter.reshape(filter_size, filter_size)
    
    # forで回しすぎて怒られそうなコードだ・・・
    converted = np.zeros(im_size*im_size).reshape(im_size, im_size)
    for i in range(im_size):
        for j in range(im_size):
            converted[i,j] = np.sum([im_lenna[i+p, j+q] * sin_filter[p, q] \
                                     for p in range(filter_size) for q in range(filter_size)])
            
    plt.figure(figsize=(7,7))
    draw_image(converted.flatten(), im_size)
    draw_image(im_lenna.flatten(), im_lenna.shape[0])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
