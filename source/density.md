---
title: density
date: 2020-05-07
---
Example Python program density.py

## Modules

* import argparse, sys, os, itertools, math
* import matplotlib, matplotlib.ticker
* from matplotlib import pyplot

## Methods

* def parse_args(args):
* def main(args):

## Code

Python example

    #!/usr/bin/env python2.7
    """
    density: plot a density plot of a file of numbers. Numbers should be floats, two
    per line.
    
    Re-uses sample code and documentation from 
    <http://users.soe.ucsc.edu/~karplus/bme205/f12/Scaffold.html>
    """
    
    import argparse, sys, os, itertools, math
    import matplotlib, matplotlib.ticker
    
    def parse_args(args):
        """
        Takes in the command-line arguments list (args), and returns a nice argparse
        result with fields for all the options.
        Borrows heavily from the argparse documentation examples:
        <http://docs.python.org/library/argparse.html>
        """
        
        # The command line arguments start with the program name, which we don't
        # want to treat as an argument for argparse. So we remove it.
        args = args[1:]
        
        # Construct the parser (which is stored in parser)
        # Module docstring lives in __doc__
        # See http://python-forum.com/pythonforum/viewtopic.php?f=3&t=36847
        # And a formatter class so our examples in the docstring look good. Isn't it
        # convenient how we already wrapped it to 80 characters?
        # See http://docs.python.org/library/argparse.html#formatter-class
        parser = argparse.ArgumentParser(description=__doc__, 
            formatter_class=argparse.RawDescriptionHelpFormatter)
        
        # Now add all the options to it
        parser.add_argument("data", type=argparse.FileType('r'),
            help="the file to read")
        parser.add_argument("--title", default="Scatterplot",
            help="the plot title")
        parser.add_argument("--x_label", default="X",
            help="the X axis label")
        parser.add_argument("--log_x", action="store_true",
            help="log X axis")
        parser.add_argument("--y_label", default="Y",
            help="the Y axis label")
        parser.add_argument("--log_y", action="store_true",
            help="log Y axis")
        parser.add_argument("--font_size", type=int, default=12,
            help="the font size for text")
        parser.add_argument("--min_x", type=float, default=None,
            help="lower limit of X axis")
        parser.add_argument("--max_x", type=float, default=None,
            help="upper limit of X axis")
        parser.add_argument("--min_y", type=float, default=None,
            help="lower limit of Y axis")
        parser.add_argument("--max_y", type=float, default=None,
            help="upper limit of Y axis")
        parser.add_argument("--save",
            help="save figure to the given filename instead of showing it")
        parser.add_argument("--dpi", type=int, default=300,
            help="save the figure with the specified DPI, if applicable")
        parser.add_argument("--sparse_ticks", action="store_true",
            help="Use sparse tick marks")
            
        return parser.parse_args(args)
        
    
    def main(args):
        """
        Parses command line arguments, and plots a histogram.
        "args" specifies the program arguments, with args[0] being the executable
        name. The return value should be used as the program's exit code.
        """
        
        options = parse_args(args) # This holds the nicely-parsed options object
        
        if options.save is not None:
            # Set up plot for use in headless mode if we just want to save. See
            # <http://stackoverflow.com/a/2766194/402891>. We need to do this before
            # we grab pyplot.
            matplotlib.use('Agg')
            
        from matplotlib import pyplot
        # Thsi holds the X coordinates for each data point
        x_data = []
        # And this holds the Y coordinates
        y_data = []
        
        for line in options.data:
            # Unpack and parse the two numbers on this line
            parts = map(float, line.split())
            
            # Put each in the appropriate list.
            x_data.append(parts[0])
            y_data.append(parts[1])
        
        # Do the plot, and grab the bin counts
        (counts, _, _, _) = pyplot.hist2d(x_data, y_data, cmap="Greens")
        # Grab the colorbar
        colorbar = pyplot.colorbar()
        # StackOverflow provides us with font sizing
        # http://stackoverflow.com/questions/3899980/how-to-change-the-font-size-on-a-matplotlib-plot
        matplotlib.rcParams.update({"font.size": options.font_size})
        pyplot.title("{} (n = {})".format(options.title, len(x_data)))
        pyplot.xlabel(options.x_label)
        if options.log_x:
            # Turn on log X axis if desired. See
            # <http://stackoverflow.com/a/3513577/402891>
            pyplot.xscale("log")
        
        pyplot.ylabel(options.y_label)
        if options.log_y:
            # And log Y axis if desired.
            pyplot.yscale("log")
        
        # Apply any range restrictions
        if(options.min_x is not None):
            pyplot.xlim((options.min_x, pyplot.xlim()[1]))    
        if(options.max_x is not None):
            pyplot.xlim((pyplot.xlim()[0], options.max_x))
            
        if(options.min_y is not None):
            pyplot.ylim((options.min_y, pyplot.ylim()[1]))    
        if(options.max_y is not None):
            pyplot.ylim((pyplot.ylim()[0], options.max_y))
            
        if options.sparse_ticks:
            # Set up tickmarks to have only 2 per axis, at the ends
            pyplot.gca().xaxis.set_major_locator(
                matplotlib.ticker.FixedLocator(pyplot.xlim()))
            pyplot.gca().yaxis.set_major_locator(
                matplotlib.ticker.FixedLocator(pyplot.ylim()))
                
            # It's a bit tricky to find the end of the colorbar. Get the max count
            # in any bin.
            colorbar.locator = matplotlib.ticker.FixedLocator((0, counts.max()))
            colorbar.update_ticks()
            
        
        # Make sure tick labels don't overlap. See
        # <http://stackoverflow.com/a/20599129/402891>
        pyplot.gca().tick_params(axis="x", pad=0.5 * options.font_size)
        
        # Make everything fit
        pyplot.tight_layout()
        
        if options.save is not None:
            # Save the figure to a file
            pyplot.savefig(options.save, dpi=options.dpi)
        else:
            # Show the figure to the user
            pyplot.show()
            
        return 0
    
    if __name__ == "__main__" :
        sys.exit(main(sys.argv))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
