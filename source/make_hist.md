---
title: make_hist
date: 2020-05-07
---
Example Python program make_hist.py

## Modules

* import matplotlib
* from matplotlib import pyplot as plt

## Methods

* def make_hist(x, title = None, xlabel = None, ylabel = None, filename = None):

## Code

Python example

    def make_hist(x, title = None, xlabel = None, ylabel = None, filename = None):
        '''
        This function generates histogram of a vector x and save to file
        Inputs:
          x: data vector
          title:    title of the plot
          xlabel:   label on x-axis
          ylabel:   label on y-axis
          filename: name of the image file (if given, save to file)
        Returns:
          matlab plot object
        Side effect:
          save an image file if filename is given
        '''
        
        import matplotlib
        matplotlib.use('agg')
        from matplotlib import pyplot as plt
        
        fig = plt.figure(figsize=(8,6))
        ax = fig.add_subplot(1, 1, 1)
        ax.hist(x, 20)
        
        if(xlabel != None):
            ax.set_xlabel(xlabel)
        if(ylabel != None):
            ax.set_ylabel(ylabel)
        if(title != None):
            ax.set_title(title)
        if(filename != None):
            fig.savefig(filename)
        
        return(fig)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
