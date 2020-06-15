---
title: matplotlib_smooth
date: 2020-05-07
---
Example Python program matplotlib_smooth.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import numpy as np
* import random
* import matplotlib
* from matplotlib.backends import qt_compat
* from PySide import QtGui, QtCore
* from PyQt4 import QtGui
* from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.backends.backend_qt4agg import NavigationToolbar2QT as NavigationToolbar
* import matplotlib.pyplot as plt
* from scipy.interpolate import spline

## Classes

* class Window(QtGui.QDialog):

## Methods

* def __init__(self, parent=None):
* def home(self):
* def zoom(self):
* def pan(self):
* def plot(self):

## Code

Example Python PyQt program :

    # !/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import sys
    import numpy as np
    import random
    import matplotlib
    
    matplotlib.use("Qt4Agg")
    from matplotlib.backends import qt_compat
    
    use_pyside = qt_compat.QT_API == qt_compat.QT_API_PYSIDE
    if use_pyside:
        from PySide import QtGui, QtCore
    else:
        from PyQt4 import QtGui
    
    from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.backends.backend_qt4agg import NavigationToolbar2QT as NavigationToolbar
    import matplotlib.pyplot as plt
    
    
    class Window(QtGui.QDialog):
        def __init__(self, parent=None):
            super(Window, self).__init__(parent)
    
            self.figure = plt.figure()
            self.canvas = FigureCanvas(self.figure)
    
            self.toolbar = NavigationToolbar(self.canvas, self)
            self.toolbar.hide()
    
            # Just some button
            self.button = QtGui.QPushButton('Plot')
            self.button.clicked.connect(self.plot)
    
            self.button1 = QtGui.QPushButton('Zoom')
            self.button1.clicked.connect(self.zoom)
    
            self.button2 = QtGui.QPushButton('Pan')
            self.button2.clicked.connect(self.pan)
    
            self.button3 = QtGui.QPushButton('Home')
            self.button3.clicked.connect(self.home)
    
            # set the layout
            layout = QtGui.QVBoxLayout()
            layout.addWidget(self.toolbar)
            layout.addWidget(self.canvas)
            layout.addWidget(self.button)
            layout.addWidget(self.button1)
            layout.addWidget(self.button2)
            layout.addWidget(self.button3)
            self.setLayout(layout)
            self.plot()
    
        def home(self):
            self.toolbar.home()
    
        def zoom(self):
            self.toolbar.zoom()
    
        def pan(self):
            self.toolbar.pan()
    
        def plot(self):
            self.figure.clf()
    
            data = [random.random() * 10 for i in range(10)]
            x = [i for i in range(10)]
    
    
            from scipy.interpolate import spline
            data = np.array(data)
            x = np.array(x)
            print(x, data)
    
            x_smooth = np.linspace(x.min(), x.max(), num=200)
            data_smooth = spline(x, data, x_smooth)
            print(x_smooth, data_smooth)
    
            ax = self.figure.add_subplot(111)
            ax.hold(True)
            ax.plot(x, data, '.-')
    
            bx = self.figure.add_subplot(111)
            bx.hold(True)
            bx.plot(x_smooth, data_smooth, '.-')
    
            self.canvas.draw()
    
    
    if __name__ == '__main__':
        app = QtGui.QApplication(sys.argv)
    
        main = Window()
        main.show()
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
