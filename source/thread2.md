---
title: thread2
date: 2020-05-07
---
Example Python program thread2.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *
* from itertools import count, islice
* from time import sleep
* from sys import exit, argv

## Classes

* class Threaded(QObject):
* class GUI(QWidget):

## Methods

* def __init__(self, parent=None, **kwargs):
* def start(self): print("Thread started")
* def loop(self):
* def stopLoop(self):
* def __init__(self, parent=None, **kwargs):
* def displayCount(self, count):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    from itertools import count, islice
    from time import sleep
    
    class Threaded(QObject):
        count=pyqtSignal(int)
    
        def __init__(self, parent=None, **kwargs):
            super().__init__(parent, **kwargs)
    
            self._count=0
            self._looping=False
    
        @pyqtSlot()
        def start(self): print("Thread started")
    
        @pyqtSlot()
        def loop(self):
            self._count=0
            self._looping=True
            while self._looping:
                self._count+=1
                self.count.emit(self._count)
                qApp.processEvents()
                sleep(1.)
    
        @pyqtSlot()
        def stopLoop(self):
            self._looping=False
    
    class GUI(QWidget):
        startLoop=pyqtSignal()
        stopLoop=pyqtSignal()
    
        def __init__(self, parent=None, **kwargs):
            super().__init__(parent, **kwargs)
    
            self._thread=QThread()
            self._threaded=Threaded(count=self.displayCount)
            self._thread.started.connect(self._threaded.start)
            self.startLoop.connect(self._threaded.loop)
            self.stopLoop.connect(self._threaded.stopLoop)
            self._threaded.moveToThread(self._thread)
            qApp.aboutToQuit.connect(self._thread.quit)
            self._thread.start()
    
            l=QVBoxLayout(self)
            l.addWidget(QPushButton("Start", self, clicked=self.startLoop))
            l.addWidget(QPushButton("Stop", self, clicked=self.stopLoop))
            self._countLbl=QLabel("Count:", self)
            l.addWidget(self._countLbl)
            
        @pyqtSlot(int)
        def displayCount(self, count):
            self._countLbl.setText("Count: {}".format(count))
    
    if __name__=="__main__":
        from sys import exit, argv
    
        a=QApplication(argv)
        g=GUI()
        g.show()
        exit(a.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
