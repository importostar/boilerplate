---
title: pyqt_threading (1)
date: 2020-05-07
---
Example Python program pyqt_threading (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import time
* from PyQt5.QtCore import (QCoreApplication, QObject, QRunnable, QThread,

## Classes

* class SomeThread(QThread):
* class SomeObject(QObject):
* class Runnable(QRunnable):

## Methods

* def run(self):
* def using_thread_subclassing():
* def some_function(self):
* def using_move_to_thread():
* def run(self):
* def using_q_runnable():

## Code

Example Python PyQt program :

    import sys
    import time
    
    from PyQt5.QtCore import (QCoreApplication, QObject, QRunnable, QThread,
                              QThreadPool, pyqtSignal)
    
    
    # Subclassing QThread
    # http://qt-project.org/doc/latest/qthread.html
    class SomeThread(QThread):
        def run(self):
            count = 0
            while count < 5:
                time.sleep(1)
                print(f"Count: {count}")
                count += 1
    
    def using_thread_subclassing():
        app = QCoreApplication([])
        thread = SomeThread()
        thread.finished.connect(app.exit)
        thread.start()
        sys.exit(app.exec_())
    
    
    # Subclassing QObject and using moveToThread
    # http://blog.qt.digia.com/blog/2007/07/05/qthreads-no-longer-abstract
    class SomeObject(QObject):
        finished = pyqtSignal()
    
        def some_function(self):
            count = 0
            while count < 5:
                time.sleep(1)
                print(f"Count: {count}")
                count += 1
            self.finished.emit()
    
    def using_move_to_thread():
        app = QCoreApplication([])
        worker_thread = QThread()
        worker = SomeObject()
        worker.moveToThread(worker_thread)
        worker.finished.connect(worker_thread.quit)
        worker_thread.started.connect(worker.some_function)
        worker_thread.finished.connect(app.exit)
        worker_thread.start()
        sys.exit(app.exec_())
    
    
    # Using a QRunnable
    # http://qt-project.org/doc/latest/qthreadpool.html
    # Note that a QRunnable isn't a subclass of QObject and therefore does
    # not provide signals and slots.
    class Runnable(QRunnable):
    
        def run(self):
            count = 0
            app = QCoreApplication.instance()
            while count < 5:
                time.sleep(1)
                print(f"Count: {count}")
                count += 1
            app.quit()
    
    def using_q_runnable():
        app = QCoreApplication([])
        runnable = Runnable()
        QThreadPool.globalInstance().start(runnable)
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
