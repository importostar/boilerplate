---
title: scratch_4
date: 2020-05-07
---
Example Python program scratch_4.py
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
* from PyQt5.QtWidgets import *

## Classes

* class WorkerSignals(QObject):
* class Worker(QRunnable):
* class Thread(object):
* class MainWindow(QMainWindow):

## Methods

* def __init__(self, fn, *args, **kwargs):
* def run(self):
* def __init__(self):
* def refresh(self) -> tuple:
* def getRefreshTime(self) -> float:
* def nextID():
* def __repr__(self):
* def __init__(self, *args, **kwargs):
* def refreshList(self):
* def refreshThreads(self):
* def processThreadRefresh(self, result):
* def addThreads(self, n=None):

## Code

Example Python PyQt program :

    import random
    import sys
    import time
    import traceback
    
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    
    
    class WorkerSignals(QObject):
        finished = pyqtSignal()
        error = pyqtSignal(tuple)
        result = pyqtSignal(tuple)
        progress = pyqtSignal(int)
    
    
    class Worker(QRunnable):
        def __init__(self, fn, *args, **kwargs):
            super(Worker, self).__init__()
    
            # Store constructor arguments (re-used for processing)
            self.fn = fn
            self.args = args
            self.kwargs = kwargs
            self.signals = WorkerSignals()
    
        @pyqtSlot()
        def run(self):
            try:
                result = self.fn(*self.args, **self.kwargs)
            except:
                traceback.print_exc()
                exctype, value = sys.exc_info()[:2]
                self.signals.error.emit((exctype, value, traceback.format_exc()))
            else:
                # print(f'Finished - {result}')
                self.signals.result.emit(result)  # Return the result of the processing
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
            return time.time() + random.uniform(3, 10)
    
        @staticmethod
        def nextID():
            Thread.i += 1
            return Thread.i
    
        def __repr__(self):
            return f'Thread(id={self.id} active={self.active})'
    
    
    class MainWindow(QMainWindow):
        def __init__(self, *args, **kwargs):
            super(MainWindow, self).__init__(*args, **kwargs)
            self.counter = 0
            # Widgets Setup
            layout = QVBoxLayout()
            self.list = QListWidget()
            self.l = QLabel("Start")
            self.button = QPushButton("Refresh List")
            self.button.pressed.connect(self.refreshList)
            layout.addWidget(self.l)
            layout.addWidget(self.button)
            layout.addWidget(self.list)
            w = QWidget()
            w.setLayout(layout)
            self.setCentralWidget(w)
            self.show()
            # Threading Setup
            self.threadpool = QThreadPool()
            print("Multithreading with maximum %d threads" % self.threadpool.maxThreadCount())
            # Refresh threads occasionally - My bad implementation
            self.rtimer = QTimer()
            self.rtimer.setInterval(1_000)
            self.rtimer.timeout.connect(self.refreshThreads) # Recheck for threads that need to be refresh()'d every second.
            # Add more threads occasionally
            self.atimer = QTimer()
            self.atimer.setInterval(5_000)
            self.atimer.timeout.connect(self.addThreads) # Add 'some' threads every 5 seconds.
            # Auto GUI List Refreshing
            self.ltimer = QTimer()
            self.ltimer.setInterval(100)
            self.ltimer.timeout.connect(self.refreshList) # Refresh GUI list every 0.1 seconds
            # Start the timers.
            self.rtimer.start()
            self.atimer.start()
            self.ltimer.start()
    
            # Thread objects (not execution threads!)
            # self.threads - A list of None and Thread objects which represent the 'active' threads in the list.
            # self.schedule - A dictionary of the UNIX timestamps the threads should be refreshed at.
            # self.working - A dictionary of bool values representing whether a thread is currently being refresh()'d.
            self.threads, self.schedule, self.working = [], {}, {}
            self.addThreads(n=10) # Add 10 threads to the list.
    
        def refreshList(self):
            # This shouldn't be central to the program's usability. Everything should process normally in the background.
            self.list.clear()
            for thread in sorted(filter(lambda x: x is not None and not self.working.get(x.id), self.threads),
                                 key=lambda t: self.schedule[t.id]):
                item = QListWidgetItem(
                    f'Thread {thread.id}/{thread.refreshes} executes in {round(self.schedule[thread.id] - time.time(), 2)}')
                self.list.addItem(item)
    
        def refreshThreads(self):
            # Schedules new workers.
    
            workers = []
            now = time.time()
            threads = filter(lambda t: t is not None and not self.working.get(t.id) and self.schedule[t.id] <= time.time(),
                             self.threads)
            for thread in threads:
                self.working[thread.id] = True
                print(f'Starting {thread}.refresh')
                worker = Worker(thread.refresh)
                worker.signals.result.connect(
                    self.processThreadRefresh)  # Once finished, the result of the refresh should be sent back.
                worker.signals.finished.connect(self.refreshList)
                workers.append(worker)
    
            # Add all the Workers to the threadpool and begin working.
            if workers:
                # print(f'Threaded {len(workers)} Workers')
                for worker in workers:
                    self.threadpool.start(worker)
    
        def processThreadRefresh(self, result):
            # Used as a way to remove threads from the running if they need to.
            # Thread callback once it returns it's result/decision.
            active, id = result
            self.working[id] = False # Stop 'working' on a thread
            if active:
                print(f'Rescheduling {self.threads[id]}')
                self.schedule[id] = self.threads[id].getRefreshTime()
            else:
                print(f'Removing {self.threads[id]}')
                self.threads[
                    id] = None  # Not really sure what to do here. double dictionary? Is a infinite list of None's okay?
                del self.schedule[id]
    
        def addThreads(self, n=None):
            # used to intermittently add new threads to the list
            new = [Thread() for _ in range(n or random.randint(1, 5))]
            self.threads.extend(new)
            for t in new:
                self.schedule[t.id] = t.getRefreshTime()
    
    
    app = QApplication([])
    window = MainWindow()
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
