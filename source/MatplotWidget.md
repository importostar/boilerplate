---
title: MatplotWidget
date: 2020-05-07
---
Example Python program MatplotWidget.py

## Modules

* from PyQt5 import QtCore, QtWidgets
* from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.backends.backend_qt5agg import NavigationToolbar2QT as NavigationToolbar
* from matplotlib.figure import Figure

## Classes

* class MplCanvas(FigureCanvas):
* class MatplotWidget(QtWidgets.QWidget):

## Methods

* 	def __init__(self, parent=None, width=5, height=4, dpi=100):
* 	def clearfig(self):
* 	def __init__(self, parent = None):

## Code

Example Python PyQt program :

    """
    ==============
    Matplot Widget
    ==============
    Matplot widget for PyQt5 apps for drawing with matplotlib.
    """
    from PyQt5 import QtCore, QtWidgets
    from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.backends.backend_qt5agg import NavigationToolbar2QT as NavigationToolbar
    from matplotlib.figure import Figure
    
    
    
    class MplCanvas(FigureCanvas):
    	def __init__(self, parent=None, width=5, height=4, dpi=100):
    		fig = Figure()
    		self.ax = fig.add_subplot(111)
    		FigureCanvas.__init__(self, fig)
    		self.setParent(parent)
    		FigureCanvas.setSizePolicy(self,
    								   QtWidgets.QSizePolicy.Expanding,
    								   QtWidgets.QSizePolicy.Expanding)
    		FigureCanvas.updateGeometry(self)
    
    
    class MatplotWidget(QtWidgets.QWidget):
    	def clearfig(self):
    		fig = self.canvas.ax.get_figure()
    		fig.clf()
    		ax = fig.add_subplot(111)
    		self.canvas.ax = ax
    
    	def __init__(self, parent = None):
    		super(MatplotWidget, self).__init__(parent)
    		self.canvas = MplCanvas()
    		self.mpl_toolbar = NavigationToolbar(self.canvas, self)
    		self.vbl = QtWidgets.QVBoxLayout()
    		self.vbl.addWidget(self.canvas)
    		self.vbl.addWidget(self.mpl_toolbar)
    		self.setLayout(self.vbl)

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
