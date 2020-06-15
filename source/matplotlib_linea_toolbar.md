---
title: matplotlib_linea_toolbar
date: 2020-05-07
---
Example Python program matplotlib_linea_toolbar.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt4 import QtCore, QtGui, uic
* from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.backends.backend_qt4agg import NavigationToolbar2QTAgg as NavigationToolbar
* import matplotlib.pyplot as plt
* import random

## Classes

* class Main(QtGui.QMainWindow, _class_ui):

## Methods

* def __init__(self, parent=None):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    """ Ejemplo Python QT.
    Añade funcionalidades a tu gráfico, como por ejemplo la exportación de imagenes, zoom, entre otros.
    Librería:
        matplotlib
    Autor:
        Diego Valladares
    Página Web:
       http://dvdeveloper.com
       http://diegovalladares.cl
    """
    import sys
    from PyQt4 import QtCore, QtGui, uic
    
    from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.backends.backend_qt4agg import NavigationToolbar2QTAgg as NavigationToolbar
    import matplotlib.pyplot as plt
    import random
    
    
    _class_ui = uic.loadUiType("ui/chart.ui")[0]
    class Main(QtGui.QMainWindow, _class_ui):
        def __init__(self, parent=None):
            QtGui.QMainWindow.__init__(self,parent)
            self.setupUi(self)
    
           	self.widget = QtGui.QWidget()
            self.layout = QtGui.QVBoxLayout(self.widget)
    
            self.figure = plt.figure()
            self.canvas = FigureCanvas(self.figure)
            self.toolbar = NavigationToolbar(self.canvas, self)
    
            self.layout.addWidget(self.toolbar)
            self.layout.addWidget(self.canvas)
    
            self.setLayout(self.layout)
            self.setCentralWidget(self.widget)
    
            data = [random.random() for i in range(10)]
            ax = self.figure.add_subplot(111)
            ax.hold(False)
            ax.plot(data, '*-')
            self.canvas.draw()
    
    app = QtGui.QApplication(sys.argv)
    MyWindow = Main(None)
    MyWindow.show()
    app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
