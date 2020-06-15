---
title: yamplot
date: 2020-05-07
---
Example Python program yamplot.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import yaml
* import matplotlib.pyplot as plt
* import sys, os

## Methods

* def plot_line(ax, line_spec):

## Code

Python example

    #!/usr/bin/env python
    
    # This is a python utility to plot data stored in a yaml file.
    # The structure of the file should be as follows:
    # An element named 'lines' which contains a sequence of lines to plot.
    # Each line should contain at least two sequence elements, labelled 'time' and 'data', with the data of the plot
    # Each line can also contain the elements labelled as matplotlib line properties (http://matplotlib.sourceforge.net/api/artist_api.html#matplotlib.lines.Line2D)
    # Optionally other elements can also be present at the root level of the yaml file:
    # An element named 'borders' containing a dict with one or more of 'top', 'bottom', 'right', 'left' elements, specifying the position of the axes borders in ratio coordinates (from 0 to 1)
    # An element named 'legend_location' containing the location of the legend as encoded in (http://matplotlib.sourceforge.net/api/axes_api.html?highlight=legend#matplotlib.axes.Axes.legend)
    # An element named 'xticks' containing a sequence of numbers where the ticks will be placed in the X axis
    # An element named 'xticklabels' containing a sequence of labels for the xticks (will only be used if 'xticks' is present and both have the same length)
    # An element named 'yticks' containing a sequence of numbers where the ticks will be placed in the Y axis
    # An element named 'yticklabels' containing a sequence of labels for the yticks (will only be used if 'yticks' is present and both have the same length)
    
    import yaml
    import matplotlib.pyplot as plt
    import sys, os
    
    def plot_line(ax, line_spec):
        data_times = line_spec['time']
        data_values = line_spec['data']
        del line_spec['data']
        del line_spec['time']
        ax.plot(data_times, data_values, **line_spec)
        
    if __name__ == '__main__':
        # Check if input arguments are provided
        if len(sys.argv) < 2:
            sys.exit('Usage: yamplot plotSpecsFile.yaml [outputFile.pdf]')
        
        # Check if plot specification file exists
        if not os.path.exists(sys.argv[1]):
            sys.exit('ERROR: Plot specification file ' + sys.argv[1] + ' not found!')
        
        # Load plot specification file
        plot_specs = yaml.load(open(sys.argv[1]))
        
        # Set default property values
        left_border = bottom_border = 0.05
        right_border = top_border = 0.99
        legend_location = 'upper right'
        xticks = None
        xticklabels = None
        yticks = None
        yticklabels = None
    
        # Get the general axes properties from yaml
        if 'borders' in plot_specs:
            plot_borders = plot_specs['borders']
            if 'left' in plot_borders:
                left_border = plot_borders['left']
            if 'right' in plot_borders:
                right_border = plot_borders['right']
            if 'top' in plot_borders:
                top_border = plot_borders['top']
            if 'bottom' in plot_borders:
                bottom_border = plot_borders['bottom']
        if 'legend_location' in plot_specs:
            legend_location = plot_specs['legend_location']
        if 'xticks' in plot_specs:
            xticks = plot_specs['xticks']
            if 'xticklabels' in plot_specs:
                xticklabels = plot_specs['xticklabels']
        if 'yticks' in plot_specs:
            yticks = plot_specs['yticks']
            if 'yticklabels' in plot_specs:
                yticklabels = plot_specs['yticklabels']
            
        
        # Create figure and axes
        fig = plt.figure()
        ax = fig.add_subplot(111)
        fig.subplots_adjust(left=left_border, bottom=bottom_border, right=right_border, top=top_border)
    
        # Plot the lines
        for line_spec in plot_specs['lines']:
            plot_line(ax, line_spec)
        
        # Format the axes labels
        if xticks is not None:
            ax.set_xticks(xticks)
            if xticklabels is not None:
                if len(xticks) != len(xticklabels):
                    print '[yamplot] Warning: \'xticklabels\' has different length than \'xticks\'. Ignoring.'
                else:
                    ax.set_xticklabels(xticklabels, size='large')
        if yticks is not None:
            ax.set_yticks(yticks)
            if yticklabels is not None:
                if len(yticks) != len(yticklabels):
                    print '[yamplot] Warning: \'yticklabels\' has different length than \'yticks\'. Ignoring.'
                else:
                    ax.set_yticklabels(yticklabels, size='large')
        
        # Plot the legend
        ax.legend(loc=legend_location)
        
        # Ouput the figure
        if len(sys.argv) > 2:
            plt.savefig(sys.argv[2])
        else:
            plt.show()
        

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
