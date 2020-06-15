---
title: LedWidget
date: 2020-05-07
---
Example Python program LedWidget.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import QSize, Qt
* from PyQt5.QtGui import QPainter, QColor
* from PyQt5.QtWidgets import QLabel, QWidget, QVBoxLayout, QApplication
* import sys

## Classes

* class Led(QWidget):
* class LedWidget(QWidget):

## Methods

* def __init__(self, colorOn, colorOff, parent=None):
* def paintEvent(self, event):
* def minimumSizeHint(self):
* def setState(self, state):
* def __init__(self, parent=None):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import QSize, Qt
    from PyQt5.QtGui import QPainter, QColor
    from PyQt5.QtWidgets import QLabel, QWidget, QVBoxLayout, QApplication
    
    
    class Led(QWidget):
        def __init__(self, colorOn, colorOff, parent=None):
            QLabel.__init__(self, parent)
            self.colorOn = colorOn
            self.colorOff = colorOff
            self.state = False
    
        def paintEvent(self, event):
            painter = QPainter(self)
            painter.setRenderHint(QPainter.Antialiasing)
            painter.setBrush(self.colorOn if self.state else self.colorOff)
            painter.drawEllipse(self.rect())
    
        def minimumSizeHint(self):
            return QSize(60, 60)
    
        def setState(self, state):
            self.state = state
    
    
    class LedWidget(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent)
            text = "TEXT"
            onColor = QColor("red")
            offColor = QColor("green")
            self.led = Led(onColor, offColor, self)
            self.setLayout(QVBoxLayout())
            self.layout().addWidget(self.led)
            label = QLabel(text, self)
            label.setAlignment(Qt.AlignCenter)
            self.layout().addWidget(label)
    
    if __name__ == "__main__":
        import sys
        app = QApplication(sys.argv)
        w = LedWidget("Text", QColor("red"), QColor("green"))
        w.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
