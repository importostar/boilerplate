---
title: pyqt5
date: 2020-05-07
---
Example Python program pyqt5.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QWidget, QPushButton, QLabel, QVBoxLayout
* from PyQt5.QtCore import pyqtSlot
* from PyQt5.QtCore import pyqtSlot, pyqtSignal, QObject
* from PyQt5.QtWidgets import QWidget, QApplication, QPushButton, QLabel, QVBoxLayout
* from PyQt5.QtCore import pyqtSignal, pyqtSlot, QThread, QObject
* import sys
* import random
* from window import Window
* from worker import WorkerObject

## Classes

* class Window(QWidget):
* class WorkerObject(QObject):
* class Main(QObject):

## Methods

* def __init__(self):
* def updateStatus(self, status):
* def __init__(self, parent=None):
* def startWork(self):
* def __init__(self, parent=None):
* def _connectSignals(self):
* def createWorkerThread(self):
* def forceWorkerReset(self):
* def forceWorkerQuit(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QWidget, QPushButton, QLabel, QVBoxLayout
    from PyQt5.QtCore import pyqtSlot
    
    class Window(QWidget):
    
        def __init__(self):
            super().__init__(self)
            self.button_start = QPushButton('Start', self)
            self.button_cancel = QPushButton('Cancel', self)
            self.label_status = QLabel('', self)
    
            layout = QVBoxLayout(self)
            layout.addWidget(self.button_start)
            layout.addWidget(self.button_cancel)
            layout.addWidget(self.label_status)
    
            self.setFixedSize(400, 200)
    
        @pyqtSlot(str)
        def updateStatus(self, status):
            self.label_status.setText(status)
    
    -----------------------------------------------------------------------------
    
    from PyQt5.QtCore import pyqtSlot, pyqtSignal, QObject
    
    class WorkerObject(QObject):
    
        signalStatus = pyqtSignal(str)
    
        def __init__(self, parent=None):
            super().__init__(parent)
    
        @pyqtSlot()
        def startWork(self):
            for ii in range(7):
                
                #self.signalStatus.emit('Iteration: {}, Factoring: {}'.format(ii, number))
                #factors = self.primeFactors(number)
                #print('Number: ', number, 'Factors: ', factors)
                self.signalStatus.emit('Idle.')
    
    
    
    -----------------------------------------------------------
    
    from PyQt5.QtWidgets import QWidget, QApplication, QPushButton, QLabel, QVBoxLayout
    from PyQt5.QtCore import pyqtSignal, pyqtSlot, QThread, QObject
    import sys
    import random
    from window import Window
    from worker import WorkerObject
    
    class Main(QObject):
    
        signalStatus = pyqtSignal(str)
    
        def __init__(self, parent=None):
            super().__init__(parent)
    
            # Create a gui object.
            self.gui = Window()
    
            # Create a new worker thread.
            self.createWorkerThread()
    
            # Make any cross object connections.
            self._connectSignals()
    
            self.gui.show()
    
    
        def _connectSignals(self):
            self.gui.button_cancel.clicked.connect(self.forceWorkerReset)
            self.signalStatus.connect(self.gui.updateStatus)
            self.parent().aboutToQuit.connect(self.forceWorkerQuit)
    
    
        def createWorkerThread(self):
    
            # Setup the worker object and the worker_thread.
            self.worker = WorkerObject()
            self.worker_thread = QThread()
            self.worker.moveToThread(self.worker_thread)
            self.worker_thread.start()
    
            # Connect any worker signals
            self.worker.signalStatus.connect(self.gui.updateStatus)
            self.gui.button_start.clicked.connect(self.worker.startWork)
    
    
        def forceWorkerReset(self):
            if self.worker_thread.isRunning():
                print('Terminating thread.')
                self.worker_thread.terminate()
    
                print('Waiting for thread termination.')
                self.worker_thread.wait()
    
                self.signalStatus.emit('Idle.')
    
                print('building new working object.')
                self.createWorkerThread()
    
    
        def forceWorkerQuit(self):
            if self.worker_thread.isRunning():
                self.worker_thread.terminate()
                self.worker_thread.wait()
    
    if __name__=='__main__':
        app = QApplication(sys.argv)
        main = Main(app)
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
