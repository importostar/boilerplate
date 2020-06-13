---
title: betterstep
date: 2020-05-07
---
Example Python program betterstep.py

## Modules

* import matplotlib.pyplot as plt

## Methods

* def betterstep(bins, y, **kwargs):

## Code

Python example

    import matplotlib.pyplot as plt
    
    def betterstep(bins, y, **kwargs):
        """A 'better' version of matplotlib's step function
        
        Given a set of bin edges and bin heights, this plots the thing
        that I wish matplotlib's ``step`` command plotted. All extra
        arguments are passed directly to matplotlib's ``plot`` command.
        
        Args:
            bins: The bin edges. This should be one element longer than
                the bin heights array ``y``.
            y: The bin heights.
            ax (Optional): The axis where this should be plotted.
        
        """
        new_x = [a for row in zip(bins[:-1], bins[1:]) for a in row]
        new_y = [a for row in zip(y, y) for a in row]
        ax = kwargs.pop("ax", plt.gca())
        return ax.plot(new_x, new_y, **kwargs)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
