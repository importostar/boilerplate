---
title: plot
date: 2020-05-07
---
Example Python program plot.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* from matplotlib.backends.backend_qt5agg import FigureCanvas
* from matplotlib.figure import Figure
* import random

## Classes

* class ApplicationWindow(QWidget):

## Methods

* def __init__(self):
* def add_pt(self):
* def update_canvas(self):

## Code

Example Python PyQt program :

    # source: https://matplotlib.org/3.1.1/gallery/user_interfaces/embedding_in_qt_sgskip.html
    
    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    
    from matplotlib.backends.backend_qt5agg import FigureCanvas
    from matplotlib.figure import Figure
    
    import random
    
    class ApplicationWindow(QWidget):
        def __init__(self):
            super().__init__()
            
            self.x = [random.randint(0, 100)]
            self.y = [random.randint(0, 100)]
    
            canvas = FigureCanvas(Figure(figsize=(5, 5)))
            self.ax = canvas.figure.subplots()
    
            add_pt_btn = QPushButton('Add point')
            add_pt_btn.clicked.connect(self.add_pt)
    
            l = QVBoxLayout(self)
            l.addWidget(canvas)
            l.addWidget(add_pt_btn)
    
            self.update_canvas()
    
        def add_pt(self):
            
            self.x.append(random.randint(0, 100))
            self.y.append(random.randint(0, 100))
            self.update_canvas()
    
        def update_canvas(self):
            self.ax.clear() # clear() reset the limits as well
            self.ax.set_xlim(xmin=0,xmax=100)
            self.ax.set_ylim(ymin=0,ymax=100)
            self.ax.scatter(self.x, self.y)
            self.ax.figure.canvas.draw()
    
    
    if __name__ == "__main__":
        qapp = QApplication(sys.argv)
        app = ApplicationWindow()
        app.show()
        qapp.exec()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
