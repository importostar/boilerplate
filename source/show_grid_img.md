---
title: show_grid_img
date: 2020-05-07
---
Example Python program show_grid_img.py

## Modules

* # Make some of the relevant imports
* import cv2 # OpenCV for perspective transform
* import numpy as np
* import matplotlib.image as mpimg
* import matplotlib.pyplot as plt
* import scipy.misc # For saving images as needed
* import glob  # For reading in a list of images from a folder

## Code

Python example

    #%matplotlib inline
    #%matplotlib qt # Choose %matplotlib qt to plot to an interactive window (note it may show up behind your browser)
    # Make some of the relevant imports
    import cv2 # OpenCV for perspective transform
    import numpy as np
    import matplotlib.image as mpimg
    import matplotlib.pyplot as plt
    import scipy.misc # For saving images as needed
    import glob  # For reading in a list of images from a folder
    
    path = './test_dataset/IMG/*'
    img_list = glob.glob(path)
    
    example_grid = './calibration_images/example_grid1.jpg'
    example_rock = './calibration_images/example_rock1.jpg'
    grid_img = mpimg.imread(example_grid)
    rock_img = mpimg.imread(example_rock)
    
    #%matplotlib notebook
    plt.imshow(grid_img)
    plt.show() 

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
