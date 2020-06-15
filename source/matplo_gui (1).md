---
title: matplo_gui (1)
date: 2020-05-07
---
Example Python program matplo_gui (1).py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtWidgets
* from matplo_ui import Ui_Form
* #below import libraries about matplotlib runing on pyqt5 
* import matplotlib
* from PyQt5 import QtCore, QtWidgets
* from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.figure import Figure
* import random
* from numpy import arange, sin, pi

## Classes

* class MyMplCanvas(FigureCanvas):
* class MyStaticMplCanvas(MyMplCanvas):
* class Form(QtWidgets.QDialog):

## Methods

* 	def __init__(self, parent=None, width=10, height=8, dpi=100):
* 	def compute_initial_figure(self):
* 	def compute_initial_figure(self):
* 	def __init__(self, parent=None):
* 	def show_graph(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5 import QtWidgets
    from matplo_ui import Ui_Form
    
    #below import libraries about matplotlib runing on pyqt5 
    import matplotlib
    #Make sure that we are using QT5
    matplotlib.use('Qt5Agg')
    from PyQt5 import QtCore, QtWidgets
    from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.figure import Figure
    
    import random
    from numpy import arange, sin, pi
    
    class MyMplCanvas(FigureCanvas):
    
    	def __init__(self, parent=None, width=10, height=8, dpi=100):
    		fig = Figure(figsize=(width, height), dpi=dpi)
    		self.axes = fig.add_subplot(111)
    
    		self.compute_initial_figure()
    
    		FigureCanvas.__init__(self, fig)
    		self.setParent(parent)
    
    		FigureCanvas.setSizePolicy(self,QtWidgets.QSizePolicy.Expanding,QtWidgets.QSizePolicy.Expanding)
    		FigureCanvas.updateGeometry(self)
    
    	def compute_initial_figure(self):
    		pass
    
    class MyStaticMplCanvas(MyMplCanvas):
    
    	def compute_initial_figure(self):
    		t = arange(0.0, 3.0, 0.01)
    		s = sin(2*pi*t)
    		self.axes.plot(t, s)
    
    
    class Form(QtWidgets.QDialog):
    	def __init__(self, parent=None):
    		super(Form, self).__init__(parent)
    		self.ui = Ui_Form()
    		self.ui.setupUi(self)
    		self.l = QtWidgets.QVBoxLayout(self.ui.widget)
    
    	def show_graph(self):
    		sc = MyStaticMplCanvas(self.ui.widget, width=5, height=4, dpi=100)
    		self.l.addWidget(sc)
    
    if __name__ == '__main__':
    	app = QtWidgets.QApplication(sys.argv)
    	window = Form()
    	window.show()
    	sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
