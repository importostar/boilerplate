---
title: AnimateMatplotlibCanvas
date: 2020-05-07
---
Example Python program AnimateMatplotlibCanvas.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from matplotlib.figure import Figure
* from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg
* from PyQt5 import QtCore
* from PyQt5.QtWidgets import QApplication, QDesktopWidget, QWidget, QSizePolicy
* from random import randint

## Classes

* class PlotCanvas(FigureCanvasQTAgg):
* class Example(QWidget):

## Methods

* def __init__(self, parent=None, width=5, height=4, dpi=100):
* def sort_shit(self, arr):
* def init_figure(self):
* def update_figure(self):
* def __init__(self):
* def center_window(self):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    import sys
    
    
    from matplotlib.figure import Figure
    from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg
    from PyQt5 import QtCore
    from PyQt5.QtWidgets import QApplication, QDesktopWidget, QWidget, QSizePolicy
    
    
    class PlotCanvas(FigureCanvasQTAgg):
    
        def __init__(self, parent=None, width=5, height=4, dpi=100):
            fig = Figure(figsize=(width, height), dpi=dpi)
            self.axes = fig.add_subplot(111)
            self.sort_func = None
            FigureCanvasQTAgg.__init__(self, fig)
            self.setParent(parent)
            FigureCanvasQTAgg.setSizePolicy(self,
                                            QSizePolicy.Expanding,
                                            QSizePolicy.Expanding)
            FigureCanvasQTAgg.updateGeometry(self)
            self.init_figure()
            self.timer = QtCore.QTimer(self)
            self.timer.timeout.connect(self.update_figure)
            self.timer.start(1500)
    
        def sort_shit(self, arr):
            for i in range(len(arr)):
                for j in range(len(arr)-1-i):
                    if arr[j] > arr[j+1]:
                        arr[j], arr[j+1] = arr[j+1], arr[j]
                        yield arr
    
        def init_figure(self):
            from random import randint
            initial_arr = [randint(-50, 50) for _ in range(5)]
            self.sort_func = self.sort_shit(initial_arr)
    
        def update_figure(self):
            try:
                arr_inst = next(self.sort_func)
                print(arr_inst)
            except StopIteration:
                self.timer.stop()
                print("Stopped timer")
                arr_inst = None
            if arr_inst:
                self.axes.cla()
                self.axes.plot(arr_inst)
                self.draw()
    
    
    class Example(QWidget):
    
        def __init__(self):
            super().__init__()
    
            self.setGeometry(300, 300, 500, 400)
            self.center_window()
            self.setWindowTitle("Shit")
            pc = PlotCanvas(self)
            self.show()
    
        def center_window(self):
            qr = self.frameGeometry()
            qr.moveCenter(QDesktopWidget().availableGeometry().center())
            self.move(qr.topLeft())
    
    
    if __name__ == "__main__":
    
        app = QApplication(sys.argv)
        ex = Example()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
