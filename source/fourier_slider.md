---
title: fourier_slider
date: 2020-05-07
---
Example Python program fourier_slider.py

## Modules

* import sys
* from PyQt5.QtWidgets import (QMainWindow, QApplication, QDockWidget, QWidget,
* from PyQt5.QtCore import Qt
* import numpy
* from numpy import sin, pi
* import matplotlib.pyplot
* import matplotlib.backends.backend_qt5agg

## Classes

* class MainWindow (QMainWindow):

## Methods

*   def __init__ (self):
*   def set_signal (self, num):
*   def plot (self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import sys
    
    from PyQt5.QtWidgets import (QMainWindow, QApplication, QDockWidget, QWidget,
                             QGridLayout, QSlider)
    from PyQt5.QtCore import Qt
    
    import numpy
    from numpy import sin, pi
    import matplotlib.pyplot
    import matplotlib.backends.backend_qt5agg
    
    class MainWindow (QMainWindow):
    
      x = numpy.linspace (0, 3, 500)
      signal = numpy.zeros_like(x)
      square = numpy.sign(sin(2*pi*x))
    
      def __init__ (self):
        QMainWindow.__init__ (self)
        self.setWindowTitle('Fourier approximation of a square wave')
        self.figure  = matplotlib.pyplot.figure ()
        self.drawing = self.figure.add_subplot (111)
        self.canvas  = matplotlib.backends.backend_qt5agg.FigureCanvasQTAgg (self.figure)
    
        self.setCentralWidget (self.canvas)
    
        dock = QDockWidget ("Value")
        self.addDockWidget (Qt.RightDockWidgetArea, dock)
    
        sliders = QWidget ()
        sliders_grid = QGridLayout (sliders)
    
        # Add slider
        sld = QSlider (Qt.Vertical, sliders)
        sld.setMinimum(1)
        sld.setTickPosition(3)
        sld.setMaximum(100)
        sld.setTickInterval(10)
        sld.valueChanged[int].connect (self.set_signal)
        sld.valueChanged.connect (self.plot)
        sliders_grid.addWidget (sld, 0, 1)
    
        dock.setWidget (sliders)
    
        self.plot ()
    
      def set_signal (self, num):
        self.signal = numpy.zeros_like(self.x)
        for k in range(1, num):
            self.signal += (4/pi)*sin(2*(2*k - 1) *pi * self.x)/(2*k - 1)
    
    
      def plot (self):
        self.drawing.hold (False)
        self.drawing.plot (self.x, self.square,
                           self.x, self.signal, '--')
        self.drawing.set_ylim (-2, 2)
        self.canvas.draw ()
    
    if __name__ == "__main__":
      app = QApplication (sys.argv)
      main = MainWindow ()
      main.show ()
      sys.exit (app.exec_ ())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
