---
title: subtitles_in_legend
date: 2020-05-07
---
Example Python program subtitles_in_legend.py

## Modules

* import matplotlib.text as mtext
* import matplotlib.pyplot as plt

## Classes

* class LegendTitle(object):

## Methods

* def __init__(self, text_props=None):
* def legend_artist(self, legend, orig_handle, fontsize, handlebox):

## Code

Python example

    # Adapted to python3 from the accepted answer on https://stackoverflow.com/questions/38463369/subtitles-within-matplotlib-legend
    # Legend guide: https://matplotlib.org/3.1.0/tutorials/intermediate/legend_guide.html
    
    
    import matplotlib.text as mtext
    
    class LegendTitle(object):
        def __init__(self, text_props=None):
            self.text_props = text_props or {}
            super(LegendTitle, self).__init__()
    
        def legend_artist(self, legend, orig_handle, fontsize, handlebox):
            x0, y0 = handlebox.xdescent, handlebox.ydescent
            title = mtext.Text(x0, y0, orig_handle, usetex=True, **self.text_props)
            handlebox.add_artist(title)
            return title
    
    
    
    if __name__ == "__main__":
    
        import matplotlib.pyplot as plt
    
        # Plots
        fig, ax = plt.subplots()
        ax.plot(range(10), label='Staff')
        ax.plot(range(10, 0, -1), 'o', color='red', label='More Staff')
    
    
        # Legend
        handles, labels = ax.get_legend_handles_labels()
    
        handles.insert(0, 'Title 1')
        labels.insert(0, '')
    
        handles.insert(2, 'Title 2')
        labels.insert(2, '')
    
        ax.legend(handles, labels, handler_map={str: LegendTitle({'fontsize': 14})})
    
    
        # Show
        plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
