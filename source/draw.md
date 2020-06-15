---
title: draw
date: 2020-05-07
---
Example Python program draw.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget
* from PyQt5.QtGui import QPainter, QPen
* from PyQt5.QtCore import Qt, QRectF, QEvent
* import signal
* import math

## Classes

* class MainWindow(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def paintEvent(self, event):
* def drawSquare(self, painter):
* def drawPoint(self, painter, x, y):
* def drawSq(self, painter, x, y, r):
* def recurDraw(self, painter, x, y, r, n):
* def eventFilter(self, source, event):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import QApplication, QWidget
    from PyQt5.QtGui import QPainter, QPen
    from PyQt5.QtCore import Qt, QRectF, QEvent
    import signal
    import math
    
    class MainWindow(QWidget):
        def __init__(self):
            super(self.__class__, self).__init__()
            self.setMouseTracking(True)
            self.installEventFilter(self)
            self.r = 100
            self.theta_left = math.acos(3/5) * 180 / math.pi
            self.initUI()
    
        def initUI(self):
            self.resize(800, 900)
            self.show()
    
        def paintEvent(self, event):
            painter = QPainter()
            painter.begin(self)
            self.drawSquare(painter)
            painter.end()
    
        def drawSquare(self, painter):
            pen = QPen(Qt.blue)
            pen.setWidth(2)
            painter.setPen(pen)
            self.recurDraw(painter, 400, 550, 100, 1)
    
        def drawPoint(self, painter, x, y):
            point = QRectF(x, y, 10, 10)
            painter.drawEllipse(point) 
    
        def drawSq(self, painter, x, y, r):
            rect = QRectF(x, y, r, r)
            painter.drawRects(rect)
    
        def recurDraw(self, painter, x, y, r, n):
    
            if n > 30:
                return
    
            """
            self.drawPoint(painter, init_x, init_y)
    
            start_x = init_x
            start_y = init_y - init_r
    
            self.drawPoint(painter, start_x, start_y)
            self.drawSq(painter, start_x, start_y, init_r)
    
            right_start_x = start_x + (4/5) * init_r * (4/5)
            right_start_y = start_y + (4/5) * init_r * (3/5)
            right_r       = init_r  * (3/5)
    
            self.drawPoint(painter, right_start_x, right_start_y)
            self.drawSq(painter, right_start_x, right_start_y, right_r)
    
            n += 1
            """
        
            print("x, y, r, n = {}, {}, {}, {}".format(x,y,r,n))
    
            k  = (4/5) ** n
    
            rect_left = QRectF(x, y, r, r)
            painter.drawRects(rect_left)
    
            painter.translate(x, y)
            painter.rotate(360 - (90 - self.theta_left))
            painter.translate(-x, -y)
    
            self.recurDraw(painter, 
                           x, 
                           y - self.r * k, 
                           self.r * k,
                           n + 1)
    
            """
            painter.rotate(-(360 - (90 - self.theta_left)))
    
            m  = (3/5) ** n
    
            rect_right = QRectF(x, y, r, r)
            painter.drawRects(rect_right)       
            painter.translate( x + r, y )
            painter.rotate(self.theta_right)
            painter.translate(-(x + r), -y)
    
            self.recurDraw(painter, (self.r - self.r * m), y - self.r * m, self.r * m, n + 1)
            """
    
        def eventFilter(self, source, event):
            if event.type() == QEvent.MouseButtonPress:
                print("x, y = {}, {}".format(event.x(), event.y()))
    
            return super(self.__class__, self).eventFilter(source, event)
    
    
    if __name__ == "__main__":
    
        # Ctrl + C
        signal.signal(signal.SIGINT, signal.SIG_DFL)
    
        app = QApplication(sys.argv)
        MainWindow = MainWindow()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
