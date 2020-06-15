---
title: arrows_on_line_ignorethis
date: 2020-05-07
---
Example Python program arrows_on_line_ignorethis.py
This program creates a PyQt GUI
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* import sys
* import logging
* import re
* import pandas as pd
* import numpy as np
* import scipy as sp
* import csv
* import bisect
* import uuid
* import matplotlib
* import colormaps
* from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.backends.backend_qt4agg import NavigationToolbar2QT as NavigationToolbar
* from matplotlib.figure import Figure
* from PySide import QtGui, QtCore
* from functools import partial
* from mat_Zerlegungen import gausselimination
* from datetime import datetime
* from mpldatacursor import datacursor

## Methods

* def main():

## Code

Python example

    import os
    import sys
    import logging
    import re
    import pandas as pd
    import numpy as np
    import scipy as sp
    import csv
    import bisect
    import uuid
    import matplotlib
    import colormaps
    
    matplotlib.use('Qt4Agg')
    matplotlib.rcParams['backend.qt4'] = 'PySide'
    from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.backends.backend_qt4agg import NavigationToolbar2QT as NavigationToolbar
    from matplotlib.figure import Figure
    from PySide import QtGui, QtCore
    from functools import partial
    from mat_Zerlegungen import gausselimination
    from datetime import datetime
    from mpldatacursor import datacursor
    
    
    def main():
        app = QtGui.QApplication.instance()  # checks if QApplication already exists
        if not app:  # create QApplication if it doesnt exist
            app = QtGui.QApplication(sys.argv)
        # Init
        widg1 = QtGui.QGroupBox(parent=None)
        vertical_layout = QtGui.QVBoxLayout(widg1)
        fig1 = Figure(dpi=72, facecolor=(1, 1, 1),
                      edgecolor=(0, 0, 0))
        canv1 = FigureCanvas(fig1)
        ax1 = fig1.add_subplot(111)
        ax1.set_xlim(-0.06, 0.06)
        ax1.set_ylim(3.35000000e-15, 3.75000000e-15)
        ax1.autoscale(True)
        transform = ax1.transData
        arrow_head = (0.5, 0.15302574986800177)
        arrow_tail = (0.0, 0.30605149973599999)
        arrow_kw = {
            'mutation_scale': 20,
            'color': [
                0.590734,
                0.152563,
                0.40029],
            'linewidth': 1.0,
            'arrowstyle': '->'}
        vertical_layout.addWidget(canv1)
        widg1.show()
        file1 = open('output_1_ignorethis.txt', 'w')
        file1.write(str(transform))
        file1.close()
        print transform
        print 'plotted successfully!'
        p = matplotlib.patches.FancyArrowPatch(
            arrow_tail, arrow_head, transform=transform,
            **arrow_kw)
        ax1.add_patch(p)
        ax1.relim()
        ax1.autoscale_view()
        canv1.draw()
        print 'patch plotted successfully!'
        # Main Loop
        app.exec_()
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
