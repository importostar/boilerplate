---
title: draw good
date: 2020-05-07
---
Example Python program draw-good.py
This program creates a PyQt GUI

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
* def patch_left(self, painter, x, y):
* def dispatch_left(self, painter, x, y):
* def patch_right(self, painter, x, y, r):
* def dispatch_right(self, painter, x, y, r):
* def recurDrawV2(self, painter, n, x, y, r, direction):
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
            self.limit = 3
            self.theta_left = math.acos(3 / 5) * 180 / math.pi
            self.theta_right = math.acos(3 / 5) * 180 / math.pi
            self.x = 440
            self.y = 550
            self.r = 100
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
            self.recurDrawV2(painter, 1, self.x, self.y, self.r, "left")
    
        def patch_left(self, painter, x, y):
            painter.translate(x, y)
            painter.rotate(360 - (90 - self.theta_left))
            painter.translate(-x, -y)
    
        def dispatch_left(self, painter, x, y):
            painter.translate(x, y)
            painter.rotate(-(360 - (90 - self.theta_left)))
            painter.translate(-x, -y)
    
        def patch_right(self, painter, x, y, r):
            painter.translate(x + r, y)
            painter.rotate(self.theta_right)
            painter.translate(-(x + r), -y)
    
        def dispatch_right(self, painter, x, y, r):
            painter.translate(x + r, y)
            painter.rotate(-self.theta_right)
            painter.translate(-(x + r), -y)
    
        def recurDrawV2(self, painter, n, x, y, r, direction):
    
            if n > self.limit:
                return
    
            else:
            
                rect_left = QRectF(x, y, r, r)
                painter.drawRects(rect_left)
                self.patch_left(painter, x, y)
                
                left_x = x
                left_y = y - r * 4/5
                left_r = r * 4/5
    
                right_x = (r - r * 3/5) + x
                right_y = y - r * 3 / 5
                right_r = r * 3 / 5
    
                self.recurDrawV2(painter, n + 1, left_x, left_y, left_r, "left")
                self.dispatch_left(painter, x, y)
                self.patch_right(painter, x, y, r)
                self.recurDrawV2(painter, n + 1, right_x, right_y, right_r, "right")
                self.dispatch_right(painter, x, y, r)
    
    
        def eventFilter(self, source, event):
            if event.type() == QEvent.MouseButtonPress:
                if event.button() == Qt.LeftButton:
                    self.limit += 1
            
                self.repaint()
    
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
