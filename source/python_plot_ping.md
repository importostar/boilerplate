---
title: python_plot_ping
date: 2020-05-07
---
Example Python program python_plot_ping.py
This program creates a PyQt GUI

## Modules

* import sys, os, random
* from PyQt4.QtCore import *
* from PyQt4.QtGui import *
* import matplotlib
* from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.backends.backend_qt4agg import NavigationToolbar2QTAgg as NavigationToolbar
* from matplotlib.figure import Figure
* import subprocess
* import re

## Classes

* class AppForm(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def on_draw(self):
* def create_main_frame(self):
* def ping(self):
* def main():

## Code

Example Python PyQt program :

    import sys, os, random
    from PyQt4.QtCore import *
    from PyQt4.QtGui import *
    
    import matplotlib
    from matplotlib.backends.backend_qt4agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.backends.backend_qt4agg import NavigationToolbar2QTAgg as NavigationToolbar
    from matplotlib.figure import Figure
    
    import subprocess
    import re
    
    class AppForm(QMainWindow):
        def __init__(self, parent=None):
            QMainWindow.__init__(self, parent)
            self.data = []
            self.setWindowTitle('Ping google result')
            self.create_main_frame()
            self.on_draw()
            self.timer = QTimer()
            self.timer.timeout.connect(self.ping)
            self.timer.start(1000)
    
        def on_draw(self):
            self.axes.clear()
            self.axes.grid(True)
    
            self.axes.plot(self.data)
    
            self.canvas.draw()
    
        def create_main_frame(self):
            self.main_frame = QWidget()
    
            self.dpi = 100
            self.fig = Figure((5.0, 4.0), dpi=self.dpi)
            self.canvas = FigureCanvas(self.fig)
            self.canvas.setParent(self.main_frame)
    
            self.axes = self.fig.add_subplot(111)
    
            self.mpl_toolbar = NavigationToolbar(self.canvas, self.main_frame)
    
            vbox = QVBoxLayout()
            vbox.addWidget(self.canvas)
            vbox.addWidget(self.mpl_toolbar)
    
            self.main_frame.setLayout(vbox)
            self.setCentralWidget(self.main_frame)
    
        def ping(self):
            host = "www.google.com"
            ping = subprocess.Popen(
                ["ping", "-c", "1", host],
                stdout = subprocess.PIPE,
                stderr = subprocess.PIPE
            )
            out, error = ping.communicate()
            m = re.search('time=(.*)ms', out)
            self.data.append(float(m.group(1)))
            self.on_draw()
    
    def main():
        app = QApplication(sys.argv)
        form = AppForm()
        form.show()
        app.exec_()
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
