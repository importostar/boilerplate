---
title: 00 startup
date: 2020-05-07
---
Example Python program 00-startup.py

## Modules

* import numpy as np
* import matplotlib as mpl
* import importlib
* from matplotlib.backends.backend_pgf import FigureCanvasPgf # For PGF or PDF export (uses TeX to render everything, no Type 3 fonts)
* import matplotlib.pyplot as plt

## Code

Python example

    # The main purpose of this file is to force matplotlib to use XeLaTeX with the fonts specified. Matplotlib's default
    # font handling for PDF is really bad on macOS and the file sizes end up being massive
    
    import numpy as np
    import matplotlib as mpl
    import importlib
    
    from matplotlib.backends.backend_pgf import FigureCanvasPgf # For PGF or PDF export (uses TeX to render everything, no Type 3 fonts)
    mpl.backend_bases.register_backend('pdf', FigureCanvasPgf)  #
    pgf_with_rc_fonts = {                                       # Comment these lines in order to go back to matplotlib's mathtex (Type 3 or Type 42 fonts)
            "font.family": "sans-serif",                        #
            "font.serif": ["TeX Gyre Pagella"],                 #
            "font.sans-serif": ["TeX Gyre Heros"],              #
            "pgf.preamble": [
                "\\usepackage{unicode-math}",
                r"\setmathfont{TeX Gyre Pagella Math}"
                ]
            }                                                   #
    mpl.rcParams.update(pgf_with_rc_fonts)                      #
    
    import matplotlib.pyplot as plt
    plt.style.use('ggplot')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
