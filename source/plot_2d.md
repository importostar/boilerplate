---
title: plot_2d
date: 2020-05-07
---
Example Python program plot_2d.py

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.animation as animation
* import math

## Methods

* def animate(i):
* def main():

## Code

Python example

    # Use 'pip install matplotlib' and be mindful of your virtual envs
    # If you want to save as GIF you will need Imagemagik
    # OSX installer: http://cactuslab.com/imagemagick/
    
    import matplotlib
    matplotlib.use("TkAgg") # default renderer breaks on xkcd styling in OSX
    
    import matplotlib.pyplot as plt
    import matplotlib.animation as animation
    import math
    
    # override the default rendering style with a better one
    plt.xkcd(scale=0.5, length=250, randomness=35)
    
    # create a window to work in
    fig = plt.figure()
    
    # create, from a 1x1 grid the first plot
    ax1 = fig.add_subplot(1,1,1)
    
    # i increments for each timestep
    def animate(i):
      # compute the values of the axis and the tick marks
      xar, yar, ticks = [], [], []
      for x in xrange(i, i + 20):
        if x % 4 == 0:
          ticks.append(x/4.0)
        xar.append(x/4.0)
        yar.append(math.sin(x/4.0))
    
      # remove any previous plots from the axes
      ax1.clear()
    
      # label all the things
      ax1.set_title("how things are gressing")
      ax1.set_xlabel("this way")
      ax1.set_ylabel("that way")
    
      # override the automatic tick marks
      plt.xticks(ticks) # calculated ticks
      plt.yticks([-0.75, 0.75]) # static ticks
      ax1.set_yticklabels(['less', 'more']) # static tick labels
    
      # create a new plot in this axes 
      ax1.plot(xar,yar)
      
      # replace the automaticly computed bounds (they shift about)
      ax1.set_xbound(xar[0], xar[-1]) # moving bounds
      ax1.set_ybound(-1.1, 1.1) # static bounds
      
    def main():
      # static
      # animate(1)
    
      # continuous
      animation.FuncAnimation(fig, animate, interval=500)
    
      # repeating (and using imagemagik to save a GIF)
      # ani = animation.FuncAnimation(fig, animate, frames=25)
      # ani.save('gressing.gif', writer='imagemagik', fps=4)
    
      plt.show()
    
    if __name__ == '__main__':
      main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
