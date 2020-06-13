---
title: WrappedText
date: 2020-05-07
---
Example Python program WrappedText.py

## Modules

* import matplotlib.pyplot as plt
* import matplotlib.text as mtext

## Classes

* class WrapText(mtext.Text):

## Methods

* def __init__(self,
* def _get_wrap_line_width(self):

## Code

Python example

    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    """
    Wrapping arbitrary text to a defined box is not supported at least up to
    Matplotlib 3.1. This is because the wrap width is hardwired to the Figure box.
    
    A way around this is to override the _get_wrap_line_width method, either with
    a new function, or by subclassing the matplotlib.text.Text class. Both
    methods are shown below.
    
    Note that this is very simple, and is not tested with rotations.
    """
    
    import matplotlib.pyplot as plt
    import matplotlib.text as mtext
    
    fig = plt.figure(1, clear=True)
    ax = fig.add_subplot(111)
    
    text = ('Lorem ipsum dolor sit amet, consectetur adipiscing elit, '
            'sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. ')
    
    # METHOD 1: OVERRIDE METHOD
    # Create a text box using fancy boxes.
    txt = ax.text(.2, .8, text, ha='left', va='top', wrap=True,
                  bbox=dict(boxstyle='square', fc='w', ec='r'))
    # Override the object's method for getting available width
    # Note width is in pixels.
    txt._get_wrap_line_width = lambda : 600.
    
    
    # METHOD 2: SUBCLASS AND CHANGE METHOD
    class WrapText(mtext.Text):
        """
        WrapText(x, y, s, width, widthcoords, **kwargs)
    
        x, y       : position (default transData)
        text       : string
        width      : box width
        widthcoords: coordinate system (default screen pixels)
        **kwargs   : sent to matplotlib.text.Text
        Return     : matplotlib.text.Text artist
        """
        def __init__(self,
                     x=0, y=0, text='',
                     width=0,
                     widthcoords=None,
                     **kwargs):
            mtext.Text.__init__(self,
                     x=x, y=y, text=text,
                     wrap=True,
                     clip_on=False,
                     **kwargs)
            if not widthcoords:
                self.width = width
            else:
                self.width = widthcoords.transform_point((width,0))[0]
    
        def _get_wrap_line_width(self):
            return self.width
    
    # Create artist object.
    wtxt = WrapText(.8, .4, text, width=.1, va='top', widthcoords=ax.transAxes,
                    bbox=dict(boxstyle='square', fc='w', ec='b'))
    # Add artist to the axes
    ax.add_artist(wtxt)
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
