---
title: async_qt5_matplotlib
date: 2020-05-07
---
Example Python program async_qt5_matplotlib.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys, random
* import asyncio
* from PyQt5.QtWidgets import *
* from quamash import QEventLoop
* from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.figure import Figure

## Classes

* class QT_app(QMainWindow, QWidget):
* class PlotCanvas(FigureCanvas):

## Methods

* def __init__(self):
* def setupUi(self):
* def start(self):
* async def main(self):
* def __init__(self, parent=None, width=5, height=4, dpi=100):
* async def ploter(self):

## Code

Example Python PyQt program :

    import sys, random
    import asyncio
    
    from PyQt5.QtWidgets import *
    from quamash import QEventLoop
    
    from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.figure import Figure
    
    class QT_app(QMainWindow, QWidget):
    
        def __init__(self):
            self.app = QApplication(sys.argv)
            self.loop = QEventLoop(self.app)
            asyncio.set_event_loop(self.loop)  # NEW must set the event loop
            super().__init__()
            self.setupUi()
            self.start()
    
        def setupUi(self):
            self.title = 'Test: pyQT5 + Matplotlib + async'
            self.width = 500
            self.height = 400
            self.left = 10
            self.top = 10
            self.setWindowTitle(self.title)
            self.setGeometry(self.left, self.top, self.width, self.height)
            self.graph = PlotCanvas(self, width=5, height=4)
            self.show()
    
        def start(self):
            with self.loop:
                self.loop.run_until_complete(self.main())
    
        async def main(self):
            while 1:
                try:
                    await self.graph.ploter()
                    await asyncio.sleep(.05)
                except:
                    break
    
    
    class PlotCanvas(FigureCanvas):
    
        def __init__(self, parent=None, width=5, height=4, dpi=100):
            fig = Figure(figsize=(width, height), dpi=dpi)
            self.axes = fig.add_subplot(111)
    
            FigureCanvas.__init__(self, fig)  # this creates self.figure??
            self.setParent(parent)
    
            FigureCanvas.setSizePolicy(self,
                                       QSizePolicy.Expanding,
                                       QSizePolicy.Expanding)
            FigureCanvas.updateGeometry(self)
            self.data = [random.random() for i in range(25)]
            self.ax = self.figure.add_subplot(111)
            self.ax.set_title('PyQt Matplotlib Async')
    
        async def ploter(self):
            self.data.append(random.random())
            self.data = self.data[-25:]
            self.ax.cla()
            self.ax.set_title('PyQt Matplotlib Async')
            self.ax.plot(self.data, 'b-')
            self.draw()
    
    
    if __name__ == '__main__':
        print('Starting App.')
        x = QT_app()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
