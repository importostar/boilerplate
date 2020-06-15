---
title: subplot_grid
date: 2020-05-07
---
Example Python program subplot_grid.py


## Methods

* def isqrt(n):
* def subplot_grid(count, rows_or_cols=True):

## Code

Python example

    def isqrt(n):
        x = n
        y = (x + 1) // 2
        while y < x:
            x = y
            y = (x + n // x) // 2
        return x
    
    def subplot_grid(count, rows_or_cols=True):
        dimension = isqrt(count)
        rows = dimension
        cols = dimension
        if (dimension**2) != count:
            if ((dimension + 1) * dimension) >= count:
                if rows_or_cols:
                    rows += 1
                else:
                    cols += 1
            else:
                rows += 1
                cols += 1
        return (rows, cols)
    
    # subplot_grid will return a squarish grid containing the number of
    # plots you want
    # the rows_or_cols tells you whether to prefer increasing rows
    # or increasing columns
    subplot_grid(5, True) # (3, 2)
    subplot_grid(5, False) # (2, 3)
    # use this with `plt.subplots()` or `fig.add_subplot()`
    # note that if you want 7 plots, you'll always get (3, 3)
    # if you then use `plt.subplots()`, you will get unnecessary axes

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
