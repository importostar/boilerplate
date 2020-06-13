---
title: pyqt_example
date: 2020-05-07
---
Example Python program pyqt_example.py
This program creates a PyQt GUI

## Modules

* import sys, random
* from PyQt4 import QtGui, QtCore
* from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.figure import Figure

## Classes

* class MplCanvas(FigureCanvas):
* class MainWindow(QtGui.QMainWindow):

## Methods

* def __init__(self, parent = None, width = 1, height = 1):
* def update_figure(self):
* def __init__(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    
    import sys, random
    
    from PyQt4 import QtGui, QtCore
    
    from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.figure import Figure
    
    class MplCanvas(FigureCanvas):
        def __init__(self, parent = None, width = 1, height = 1):
            figure = Figure(figsize = (width, height))
            self.axes = figure.add_subplot(111)
            # We want the axes cleared every time plot() is called
            self.axes.hold(False)
    
            FigureCanvas.__init__(self, figure)
            self.setParent(parent)
    
            FigureCanvas.setSizePolicy(self, QtGui.QSizePolicy.Expanding, QtGui.QSizePolicy.Expanding)
            FigureCanvas.updateGeometry(self)
    
            self.update_figure()
            timer = QtCore.QTimer(self)
            timer.timeout.connect(self.update_figure)
            timer.start(1000)
    
        def update_figure(self):
            num_ints = 10
            random_ints = [ random.randint(0, 10) for i in range(num_ints) ]
            self.axes.plot(range(num_ints), random_ints, 'r')
            self.draw()
    
    class MainWindow(QtGui.QMainWindow):
        def __init__(self):
            QtGui.QMainWindow.__init__(self)
    
            self.setAttribute(QtCore.Qt.WA_DeleteOnClose) # Garbage-collect the window after it's been closed.
            self.setWindowTitle("Test window")
    
            main_widget = QtGui.QWidget(self)
            self.setCentralWidget(main_widget)
    
            box_layout = QtGui.QVBoxLayout(main_widget)
    
            canvas = MplCanvas(main_widget)
            box_layout.addWidget(canvas)
    
            self.show()
    
    app = QtGui.QApplication(sys.argv)
    app_window = MainWindow()
    sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
