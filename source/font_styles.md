---
title: font_styles
date: 2020-05-07
---
Example Python program font_styles.py

## Modules

* import matplotlib
* from matplotlib import _get_data_path
* from matplotlib.font_manager import FontProperties, findfont
* import matplotlib.pyplot as plt

## Methods

* def find_matplotlib_font(**kw):

## Code

Python example

    import matplotlib
    matplotlib.use("Agg")
    
    from matplotlib import _get_data_path
    data_path = _get_data_path()
    
    def find_matplotlib_font(**kw):
        prop = FontProperties(**kw)
        path = findfont(prop, directory=data_path)
        return FontProperties(fname=path)
    
    from matplotlib.font_manager import FontProperties, findfont
    import matplotlib.pyplot as plt
    
    fig = plt.figure()
    ax = plt.subplot( 1, 1, 1 )
    
    normalFont = find_matplotlib_font( family = "sans-serif",
                                       style = "normal",
                                       variant = "normal",
                                       size = 14,
                                       )
    ax.annotate( "Normal Font", (0.1, 0.1), xycoords='axes fraction',
                  fontproperties = normalFont )
    
    boldFont = find_matplotlib_font( family = "Foo",
                                     style = "normal",
                                     variant = "normal",
                                     weight = "bold",
                                     stretch = 500,
                                     size = 14,
                                     )
    ax.annotate( "Bold Font", (0.1, 0.2), xycoords='axes fraction',
                  fontproperties = boldFont )
    
    boldItemFont = find_matplotlib_font( family = "sans serif",
                                         style = "italic",
                                         variant = "normal",
                                         weight = 750,
                                         stretch = 500,
                                         size = 14,
                                         )
    ax.annotate( "Bold Italic Font", (0.1, 0.3), xycoords='axes fraction',
                  fontproperties = boldItemFont )
    
    lightFont = find_matplotlib_font( family = "sans-serif",
                                      style = "normal",
                                      variant = "normal",
                                      weight = 200,
                                      stretch = 500,
                                      size = 14,
                                      )
    ax.annotate( "Light Font", (0.1, 0.4), xycoords='axes fraction',
                  fontproperties = lightFont )
    
    condensedFont = find_matplotlib_font( family = "sans-serif",
                                          style = "normal",
                                          variant = "normal",
                                          weight = 500,
                                          stretch = 100,
                                          size = 14,
                                          )
    ax.annotate( "Condensed Font", (0.1, 0.5), xycoords='axes fraction',
                  fontproperties = condensedFont )
    
    ax.set_xticks([])
    ax.set_yticks([])
    
    fig.savefig("test.png")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
