---
title: scratch_8
date: 2020-05-07
---
Example Python program scratch_8.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random
* import sys
* import time
* import traceback
* from PyQt5.QtCore import *
* from PyQt5.QtGui import QFont
* from PyQt5.QtWidgets import *

## Classes

* class WorkerSignals(QObject):
* class Worker(QRunnable):
* class Thread(object):
* class MainWindow(QMainWindow):

## Methods

* def __init__(self, obj, *args, **kwargs):
* def run(self):
* def __init__(self):
* def refresh(self) -> tuple:
* def getRefreshTime(self) -> float:
* def nextID():
* def __repr__(self):
* def __init__(self, *args, **kwargs):
* def refreshList(self):
* def refreshResult(self, result):
* def updateActivity(self, id):
* def addToPool(self, thread, restart=False):
* def activeThreads(self):
* def addThreads(self):

## Code

Example Python PyQt program :

    import random
    import sys
    import time
    import traceback
    
    from PyQt5.QtCore import *
    from PyQt5.QtGui import QFont
    from PyQt5.QtWidgets import *
    
    
    class WorkerSignals(QObject):
        finished = pyqtSignal()
        starting = pyqtSignal(int)
        result = pyqtSignal(tuple)
    
    class Worker(QRunnable):
        def __init__(self, obj, *args, **kwargs):
            super(Worker, self).__init__()
    
            # Store constructor arguments (re-used for processing)
            self.obj = obj
            self.args = args
            self.kwargs = kwargs
            self.signals = WorkerSignals()
    
        @pyqtSlot()
        def run(self):
            try:
                wait = self.obj.getRefreshTime()
                print(f'Thread {self.obj.id} sleeping for {wait} seconds.')
                time.sleep(wait)
                self.signals.starting.emit(self.obj.id)
                result = self.obj.refresh(*self.args, **self.kwargs)
                print(f'Thread {self.obj.id} finished.')
                self.signals.result.emit(result)  # Return the result of the processing
            except:
                traceback.print_exc()
            finally:
                self.signals.finished.emit()  # Done
    
    
    class Thread(object):
        """
        Basic Rules for a Thread Object:
        Cannot store the next timestamp on the object (it's a database object, I don't believe it's good practice
        to be creating sessions over and over to simply read/write the access time.
        ID and Active are allowed as booleans.
        """
        i = -1
    
        def __init__(self):
            self.id = Thread.nextID()
            self.active = True
            self.refreshes = 0
    
        def refresh(self) -> tuple:
            # Represents my SQL Alchemy Model's refresh() function
            self.refreshes += 1
            time.sleep(random.randint(2, 5))
            if random.random() <= max(0.1, 1.0 - ((self.refreshes + 5) / 10)):
                self.active = False
            return self.active, self.id
    
        def getRefreshTime(self) -> float:
            # Provides the next interval this thread should wait before refresh() should be called.
            # Should NOT be used to determine whether the thread is still active or not.
            return random.uniform(3, 10)
    
        @staticmethod
        def nextID():
            Thread.i += 1
            return Thread.i
    
        def __repr__(self):
            return f'Thread(id={self.id} active={self.active})'
    
    
    class MainWindow(QMainWindow):
        def __init__(self, *args, **kwargs):
            super(MainWindow, self).__init__(*args, **kwargs)
    
            # Widgets Setup
            layout = QVBoxLayout()
            self.list = QListWidget()
            self.l = QLabel("Total Active: 0")
            self.button = QPushButton("Refresh List")
            self.button.pressed.connect(self.refreshList)
            self.button.setDisabled(True)
            layout.addWidget(self.l)
            layout.addWidget(self.button)
            layout.addWidget(self.list)
            w = QWidget()
            w.setLayout(layout)
            self.setCentralWidget(w)
            self.show()
    
            self.atimer = QTimer()
            self.atimer.setInterval(5_000)
            self.atimer.timeout.connect(self.addThreads)
    
            # Threading Setup
            self.threadpool = QThreadPool()
            print("Multithreading with maximum %d threads" % self.threadpool.maxThreadCount())
    
            self.active = []
            self.threads = []
            # self.addToPool([Thread() for _ in range(random.randint(20, 45))])
            self.atimer.start()
    
        def refreshList(self):
            # This shouldn't be central to the program's usability. Everything should process normally in the background.
            self.list.clear()
            bold = QFont()
            bold.setBold(True)
            active = 0
            for thread in filter(lambda t : t.active, self.threads):
                item = QListWidgetItem(
                    f'Thread {thread.id}/{thread.refreshes}')
                if self.active[thread.id]:
                    active += 1
                    item.setFont(bold)
                self.list.addItem(item)
            self.l.setText(f'Total Active: {active}/{len(list(filter(lambda t : t.active, self.threads)))}')
    
        def refreshResult(self, result):
            self.active[result[1]] = False
            if result[0]:
                print(f'Restarting Thread {result[1]}')
                self.addToPool([self.threads[result[1]]], restart=True) # Add by ID, which would normally be a database GET
            else:
                print(f'Thread {result[1]} shutting down.')
            self.refreshList()
    
        def updateActivity(self, id):
            print(f'Thread {id} is starting.')
            self.active[id] = True
            self.refreshList()
    
        def addToPool(self, thread, restart=False):
            if type(thread) is list:
                for subthread in thread:
                    self.addToPool(subthread, restart=restart)
            else:
                if not restart:
                    self.active.append(False)
                    self.threads.append(thread)
                print(f'Adding to pool - {thread.id}')
                worker = Worker(thread)
                worker.signals.result.connect(self.refreshResult)
                worker.signals.starting.connect(self.updateActivity)
                self.threadpool.start(worker)
            self.refreshList()
    
        @property
        def activeThreads(self):
            return list(filter(lambda t : self.active[t.id], self.threads))
    
        def addThreads(self):
            print('Adding Threads...')
            target = 25 + random.randint(-10, 8)
            add = target - len(self.threads)
            if add > 0:
                print(f'Adding {add} thread{"s" if add > 1 else ""} to pool.')
                self.addToPool([Thread() for _ in range(add)])
    
    app = QApplication([])
    window = MainWindow()
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
