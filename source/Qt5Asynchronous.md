---
title: Qt5Asynchronous
date: 2020-05-07
---
Example Python program Qt5Asynchronous.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import time
* from PyQt5.QtCore import pyqtSlot, pyqtSignal, QThread
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton

## Classes

* class HeavyComputationThread(QThread):
* class AppWidget(QWidget):

## Methods

* def __init__(self, x, y):
* def run(self):
* def stop(self):
* def __init__(self):
* def start(self):
* def result_ready(self, result):
* def cancel(self):

## Code

Example Python PyQt program :

    import sys
    import time
    
    from PyQt5.QtCore import pyqtSlot, pyqtSignal, QThread
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton
    
    """
    Example how to make asynchronous computation in PyQt5
    """
    
    
    class HeavyComputationThread(QThread):
        """
        Thread performing the computation
        """
    
        # setup a signal, which takes a single object as parameter
        resultAvailable = pyqtSignal(object)
    
        def __init__(self, x, y):
            QThread.__init__(self)
            self.x = x
            self.y = y
    
            # mark the thread is alive
            self.alive = True
    
        # called when the thread starts running
        def run(self):
            # compute something
            sum = self.x + self.y
    
            # simulated delay
            for i in range(1, 6):
                print(f"Thread :: sleeping {i}")
                time.sleep(1)
    
                # make the thread interruptible - check the alive flag regularly if possible
                if not self.alive:
                    break
    
            if not self.alive:
                print("Thread :: Computation cancelled")
                return
    
            print(f"Thread :: computation finished, sum is {sum}")
    
            # result can be complex, as an example I am passing a dictionary
            result = {
                'x': self.x,
                'y': self.y,
                'sum': sum
            }
    
            # emit result to the AppWidget
            self.resultAvailable.emit(result)
    
        def stop(self):
            # mark this thread as not alive
            self.alive = False
            # wait for it to really finish
            self.wait()
    
    
    class AppWidget(QWidget):
        """
        Main (and only ;) ) UI element
        """
    
        def __init__(self):
            QWidget.__init__(self)
            self.resize(225, 100)
            self.setWindowTitle('Start async')
    
            # slot for the running thread, empty now
            self.running_thread = None
    
            self.startButton = QPushButton('Start computation', self)
            self.startButton.move(10, 50)
            self.startButton.clicked.connect(self.start)  # register onClick callback
    
            self.cancelButton = QPushButton('Cancel', self)
            self.cancelButton.move(130, 50)
            self.cancelButton.clicked.connect(self.cancel)  # register onClick callback
            self.cancelButton.setEnabled(False)
    
        @pyqtSlot()
        def start(self):
            """
            onclick callback of the startButton
            """
            print('UI :: Starting the computation')
            self.startButton.setEnabled(False)
            self.cancelButton.setEnabled(True)
    
            # create a background thread, execute something on it
            self.running_thread = HeavyComputationThread(31, 11)
            self.running_thread.resultAvailable.connect(self.result_ready)  # register a callback method
            self.running_thread.start()
    
        @pyqtSlot(object)
        def result_ready(self, result):
            """
            called when the computation is finished
            :param result: result of the computation
            """
            print(f"UI :: Received result {result}")
            self.startButton.setEnabled(True)
            self.cancelButton.setEnabled(False)
            self.running_thread = None
    
        @pyqtSlot()
        def cancel(self):
            print('UI :: Cancelling the thread')
            """
            onclick callback of the cancelButton
            """
            self.running_thread.stop()
            print('UI :: Thread cancelled')
            self.startButton.setEnabled(True)
            self.cancelButton.setEnabled(False)
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        w = AppWidget()
        w.show()
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
