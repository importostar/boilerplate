---
title: image_example
date: 2020-05-07
---
Example Python program image_example.py

## Modules

* from matplotlib import pyplot as plt # the standard python plotting library
* import numpy as np # math library for data-handling

## Methods

* def rgb2gray(rgb):

## Code

Python example

    from matplotlib import pyplot as plt # the standard python plotting library
    # installation instructions here: https://github.com/matplotlib/matplotlib
    import numpy as np # math library for data-handling
    
    # DEMO on random matrix to show how filtering based on pixel intensity works. How to make an image. 
    n = 20
    I = np.random.random((n, n))
    I[I>0.5] = 1 # highpass filter in two lines of code.
    I[I<0.5] = 0 
    
    colormap = plt.cm.gray # any of these: https://matplotlib.org/users/colormaps.html
    plt.imshow(I, cmap=colormap) # plot in Black and White
    # this line below tells matplotlib "I'm done constructing my image (titles, labels, etc.), now show me it." sometimes unecessary. depends on how you're interacting with python
    plt.show() 
    
    # HOW TO LOAD A FILE
    filename = 'myfile.png'
    I = plt.imread(filename) # this is how to load an image
    plt.imshow(I) 
    plt.title('Original Image'); plt.ylabel('px'); plt.xlabel('px');
    plt.show()
    
    
    
    # CONVERT image to grayscale
    def rgb2gray(rgb):
        r, g, b = rgb[:,:,0], rgb[:,:,1], rgb[:,:,2]
        gray = 0.2989 * r + 0.5870 * g + 0.1140 * b
        return gray
    
    G = rgb2gray(I)
    # OPTIONAL - CROPPING
    # G = G[375:1175,330:950] # overwrite image with cropped version
    plt.imshow(G)
    plt.show()
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
