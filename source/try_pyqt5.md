---
title: try_pyqt5
date: 2020-05-07
---
Example Python program try_pyqt5.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QMainWindow, QLabel
* from PyQt5.QtGui import QPainter, QPen
* from PyQt5.QtCore import QTimer, Qt

## Classes

* class MainWindow(QMainWindow):

## Methods

* def __init__(self):
* def updateCount(self):
* def paintEvent(self, event):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    
    import sys
    from PyQt5.QtWidgets import QApplication, QMainWindow, QLabel
    from PyQt5.QtGui import QPainter, QPen
    from PyQt5.QtCore import QTimer, Qt
    
    class MainWindow(QMainWindow):
      # constructor
        def __init__(self):
            QMainWindow.__init__(self)
            # counter
            self.i = 0
            self.width = 500
            self.height = 500
            self.setGeometry(0, 0, self.width, self.height)
            # make QTimer
            self.qTimer = QTimer()
            # set interval to 1 s
            self.qTimer.setInterval(1000) # 1000 ms = 1 s
            # connect timeout signal to signal handler
            self.qTimer.timeout.connect(self.updateCount)
            # start timer
            self.qTimer.start()
    
        def updateCount(self):
            self.i += 1
            self.update()
    
        def paintEvent(self, event):
            painter = QPainter(self)
            painter.setPen(QPen(Qt.green,  8, Qt.DashLine))
            for i in range(self.i):
                painter.drawEllipse(40 + i * 50, 40, 400, 400)
    
    qApp = QApplication(sys.argv)
    # setup GUI
    qWin = MainWindow()
    qWin.show()
    # run application
    sys.exit(qApp.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
