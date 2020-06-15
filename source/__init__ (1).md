---
title: __init__ (1)
date: 2020-05-07
---
Example Python program __init__ (1).py


## Methods

* def _line_division(chart, ax):

## Code

Python example

    def _line_division(chart, ax):
        """Convert encodings, manipulate data if needed, plot on ax.
        Parameters
        ----------
        chart : altair.Chart
            The Altair chart object
        ax
            The Matplotlib axes object
        Notes
        -----
        Fill isn't necessary until mpl-altair can handle multiple plot types in one plot.
        Size is unsupported by both Matplotlib and Altair.
        When both Color and Stroke are provided, color is ignored and stroke is used.
        Shape is unsupported in line graphs unless another plot type is plotted at the same time.
        Opacity still needs to be implemented.
        """
        if chart.to_dict()['encoding'].get('opacity'):
            raise NotImplementedError("Still need to implement.")
            # dtype = _locate_channel_dtype(chart, 'opacity')
            # normalize opacity values to (0,1)
            # mapping['kwargs'] = {'alpha': normalized_vals}  # ish (not really going to work)
    
        if chart.to_dict()['encoding'].get('stroke'):
            grouping = chart.to_dict()['encoding']['stroke']['field']
        elif chart.to_dict()['encoding'].get('color'):  # If both color and stroke are encoded, color is ignored.
            grouping = chart.to_dict()['encoding']['color']['field']
        else:
            mapping = _convert(chart)
            ax.plot(*mapping['args'])
            return
    
        for lab, subset in chart.data.groupby(grouping):
            tmp_chart = chart
            tmp_chart.data = subset
            mapping = _convert(tmp_chart)
            mapping['kwargs'] = {'label': lab}  # for legend purposes later on
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
