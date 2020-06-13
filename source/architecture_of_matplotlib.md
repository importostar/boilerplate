---
title: architecture_of_matplotlib
date: 2020-05-07
---
Example Python program architecture_of_matplotlib.py

## Modules

* import numpy as np
* from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
* from matplotlib.figure import Figure

## Code

Python example

    # A simple Python script illustrating the architecture of matplotlib.
    # It defines the backend, connects a Figure to it,
    #  uses the array library numpy to create 10,000 normally distributed random
    #  numbers, and plots a histogram of these.
    # http://www.aosabook.org/en/matplotlib.html
    
    # Import the FigureCanvas from the backend of your choice
    #  and attach the Figure artist to it.
    import numpy as np
    from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
    from matplotlib.figure import Figure
    fig = Figure()
    canvas = FigureCanvas(fig)
    
    # Import the numpy library to generate the random numbers.
    x = np.random.randn(10000)
    
    # Now use a figure method to create an Axes artist; the Axes artist is
    #  added automatically to the figure container fig.axes.
    # Here "111" is from the MATLAB convention: create a grid with 1 row and 1
    #  column, and use the first cell in that grid for the location of the new
    #  Axes.
    ax = fig.add_subplot(111)
    
    # Call the Axes method hist to generate the histogram; hist creates a
    #  sequence of Rectangle artists for each histogram bar and adds them
    #  to the Axes container.  Here "100" means create 100 bins.
    ax.hist(x, 100)
    
    # Decorate the figure with a title and save it.
    ax.set_title('Normal distribution with $\mu=0, \sigma=1$')
    fig.savefig('matplotlib_histogram.png')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
