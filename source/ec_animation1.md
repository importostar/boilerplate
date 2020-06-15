---
title: ec_animation1
date: 2020-05-07
---
Example Python program ec_animation1.py

## Modules

* # step 1: import the animation module
* import matplotlib.animation as animation
* import numpy as np
* import matplotlib.pyplot as plt
* # another way to import:
* # from matplotlib animation import FuncAnimation

## Methods

* def update(curr):  #? how the info about the curr can be passed? 

## Code

Python example

    # Modified from Coursera
    
    # how to do an animation in matplotlib:
    
    # step 1: import the animation module
    import matplotlib.animation as animation
    import numpy as np
    import matplotlib.pyplot as plt
    # another way to import:
    # from matplotlib animation import FuncAnimation
    
    
    # step 2: define the number of frames. 
    n = 100
    
    # step 3: prepare the data to plot 
    # draw sample from standardized normal distribution
    x = np.random.randn(n) 
    
    
    # step 4: prep the figure
    fig = plt.figure()
    
    
    # step 5: prep the callable function that will do the plotting
    # the argument must be the next value in frames
    def update(curr):  #? how the info about the curr can be passed? 
        # check if animation is at the last frame, and if so, stop the animation a. 
        if curr == n:
            a.event_source.stop() 
        plt.cla()  # each iteration will draw a new axes (frame), thus we have to clear the prev frame first
        bins = np.arange(-4, 4, 0.5)  # the bins edge range from -4 to 4 with a step of 0.5
        plt.hist(x[:curr], bins=bins) # each iteration will plot the 0th - the(curr-1)th elements of the list x. 
                                      # thus, data plotted in current iteration = data plotted in prev iteration + 1
        plt.axis([-4, 4, 0, 30]) # set the lim for x & y axis
        plt.gca().set_title('Sampling the Normal Distribution') # plot title
        plt.gca().set_ylabel('Frequency') # y axis title
        plt.gca().set_xlabel('Value') # x axis title
        plt.annotate('n = {}'.format(curr), [3, 27]) # give annotation to the plot. --> similar to plt.text. 
    
    # step 6: create the animation by calling the FuncAnimation
    a = animation.FuncAnimation(fig, update, interval=100)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
