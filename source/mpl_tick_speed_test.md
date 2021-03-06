---
title: mpl_tick_speed_test
date: 2020-05-07
---
Example Python program mpl_tick_speed_test.py
This program creates a PyQt GUI
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import time
* import numpy
* from PySide import QtCore, QtGui
* import matplotlib
* import matplotlib.ticker
* from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.figure import Figure

## Classes

* class Graph(QtGui.QWidget):

## Methods

* def __init__(self, parent=None):
* def present_axis(self):
* def test_fps(self):
* def _internal_test(self):

## Code

Python example

    import time
    import numpy
    from PySide import QtCore, QtGui
    import matplotlib
    import matplotlib.ticker
    matplotlib.use('Qt4Agg')
    from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.figure import Figure
    
    class Graph(QtGui.QWidget):
        def __init__(self, parent=None):
            super(Graph, self).__init__(parent)
    
            self.figure = Figure(figsize=(600, 600), dpi=72, facecolor=(1, 1, 1), edgecolor=(0, 0, 0), tight_layout=True)
            self.canvas = FigureCanvas(self.figure)
            self.ax = self.figure.add_subplot(1, 1, 1)
    
            self.layout = QtGui.QVBoxLayout(self)
    
            self.header = QtGui.QHBoxLayout()
    
            self.form = QtGui.QFormLayout()
            self.num_points_edit = QtGui.QLineEdit()
            self.num_points_edit.setText('100')
            self.num_points_edit.editingFinished.connect(self.present_axis)
            self.num_ticks_edit = QtGui.QLineEdit()
            self.num_ticks_edit.setText('10')
            self.num_ticks_edit.editingFinished.connect(self.present_axis)
            self.form.addRow('Points', self.num_points_edit)
            self.form.addRow('Ticks', self.num_ticks_edit)
    
            self.header.addLayout(self.form)
            self.commands = QtGui.QDialogButtonBox(QtCore.Qt.Vertical)
            self.commands.addButton('Test FPS', QtGui.QDialogButtonBox.ActionRole).clicked.connect(self.test_fps)
            self.header.addWidget(self.commands)
    
            self.layout.addLayout(self.header)
            self.layout.addWidget(self.canvas)
    
        def present_axis(self):
            self.points = int(self.num_points_edit.text())
            self.ticks = int(self.num_ticks_edit.text())
    
            if hasattr(self, 'scat'):
                self.scat.remove()
    
            self.scat = self.ax.scatter(numpy.arange(self.points), numpy.sin(numpy.arange(self.points)))
            self.ax.xaxis.set_minor_locator(matplotlib.ticker.LinearLocator(self.ticks))
            self.ax.yaxis.set_minor_locator(matplotlib.ticker.LinearLocator(self.ticks))
            self.canvas.draw()
    
        def test_fps(self):
            self.start_test = time.time()
            self.test_count = 0
            QtCore.QTimer.singleShot(0, self._internal_test)
    
        def _internal_test(self):
            now = time.time()
            if now - self.start_test > 1.:
                print 'Points:  {}; Ticks:  {};  FPS:  {}'.format(self.points, self.ticks, self.test_count)
                return
            self.canvas.draw()
            self.test_count += 1
            QtCore.QTimer.singleShot(0, self._internal_test)
    
    app = QtGui.QApplication([])
    w = QtGui.QMainWindow()
    w.setCentralWidget(Graph())
    w.show()
    app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
