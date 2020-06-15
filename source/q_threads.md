---
title: q_threads
date: 2020-05-07
---
Example Python program q_threads.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* from PyQt5.QtCore import QObject
* from PyQt5.QtCore import QThread
* from PyQt5.QtCore import pyqtSignal
* from PyQt5.QtCore import pyqtSlot
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtWidgets import QHBoxLayout
* from PyQt5.QtWidgets import QMainWindow
* from PyQt5.QtWidgets import QPushButton
* from PyQt5.QtWidgets import QWidget
* import sys

## Classes

* class MyApplication(QMainWindow):
* class Runnable(QObject):
* class ExtendingThread(QThread, Runnable):
* class Associable(Runnable):

## Methods

* def __init__(self):
* def _a_slot(self, who):
* def extend(self):
* def associate(self):
* def run(self):
* def run(self):

## Code

Example Python PyQt program :

    """
    Show the differences in behaviour between associating and inheriting qthreads
    """
    import time
    
    from PyQt5.QtCore import QObject
    from PyQt5.QtCore import QThread
    from PyQt5.QtCore import pyqtSignal
    from PyQt5.QtCore import pyqtSlot
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtWidgets import QHBoxLayout
    from PyQt5.QtWidgets import QMainWindow
    from PyQt5.QtWidgets import QPushButton
    from PyQt5.QtWidgets import QWidget
    
    
    class MyApplication(QMainWindow):
        def __init__(self):
            super(MyApplication, self).__init__()
            self.extend_run = QPushButton("Extend run")
            self.use_association = QPushButton("Use associated object")
            self.__extended = ExtendingThread()
            self.__associated = QThread()
            self.__runnable = Associable()
            self.__runnable.moveToThread(self.__associated)
            self.__runnable.signal_.connect(self._a_slot)
            self.__associated.started.connect(self.__runnable.run)
    
            self.extend_run.clicked.connect(self.extend)
            self.__extended = ExtendingThread()
            self.__extended.signal_.connect(self._a_slot)
    
            self.use_association.clicked.connect(self.associate)
            la = QHBoxLayout()
            for x in [self.extend_run, self.use_association]:
                la.addWidget(x)
            self.cw = QWidget()
            self.cw.setLayout(la)
            self.setCentralWidget(self.cw)
            print("Main: %s" % self.thread())
    
        @pyqtSlot(str)
        def _a_slot(self, who):
            th = str(self.thread())
            print("*\n{}\n{}\n{}*".format(who, th, who == th))
    
        def extend(self):
            print(self.extend_run.text(), ':', self.thread())
            self.__extended.start()
    
        def associate(self):
            print(self.use_association.text(), ':', self.thread())
            self.__associated.start()
    
    
    class Runnable(QObject):
        signal_ = pyqtSignal(str)
    
        def run(self):
            for x in range(1, 4):
                time.sleep(1)
                self.signal_.emit(str(self.thread()))
    
    
    class ExtendingThread(QThread, Runnable):
        signal_ = pyqtSignal(str)
    
    
    class Associable(Runnable):
        def run(self):
            super(Associable, self).run()
            # Must explicitly tell the event loop in the thread to stop
            self.thread().exit(0)
    
    
    if __name__ == '__main__':
        import sys
    
        app = QApplication(sys.argv)
        mai = MyApplication()
        mai.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
