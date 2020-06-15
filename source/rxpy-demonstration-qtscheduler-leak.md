---
title: rxpy demonstration qtscheduler leak
date: 2020-05-07
---
Example Python program rxpy-demonstration-qtscheduler-leak.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import rx
* from rx import operators as ops
* from rx.subjects import Subject
* from rx.concurrency.mainloopscheduler import QtScheduler
* from PyQt5 import QtCore
* from PyQt5.QtWidgets import QApplication, QWidget, QLabel
* from PySide2 import QtCore
* from PySide2.QtWidgets import QApplication, QLabel, QWidget
* from PyQt4 import QtCore
* from PyQt4.QtGui import QWidget, QLabel, QApplication
* from PySide import QtCore
* from PySide.QtGui import QWidget, QLabel, QApplication

## Classes

* class Window(QWidget):

## Methods

* def __init__(self):
* def mouseMoveEvent(self, event):
* def main():
* def on_next(info):
* def handle_label(label, i):

## Code

Example Python PyQt program :

    import sys
    
    import rx
    from rx import operators as ops
    from rx.subjects import Subject
    from rx.concurrency.mainloopscheduler import QtScheduler
    
    try:
        from PyQt5 import QtCore
        from PyQt5.QtWidgets import QApplication, QWidget, QLabel
    except ImportError:
        try:
            from PySide2 import QtCore
            from PySide2.QtWidgets import QApplication, QLabel, QWidget
        except ImportError:
            try:
                from PyQt4 import QtCore
                from PyQt4.QtGui import QWidget, QLabel, QApplication
            except ImportError:
                from PySide import QtCore
                from PySide.QtGui import QWidget, QLabel, QApplication
    
    
    class Window(QWidget):
    
        def __init__(self):
            QWidget.__init__(self)
            self.setWindowTitle("Rx for Python rocks")
            self.resize(600, 600)
            self.setMouseTracking(True)
    
            # This Subject is used to transmit mouse moves to labels
            self.mousemove = Subject()
    
        def mouseMoveEvent(self, event):
            self.mousemove.on_next((event.x(), event.y()))
    
    
    def main():
        app = QApplication(sys.argv)
        scheduler = QtScheduler(QtCore)
    
        window = Window()
        window.show()
    
        text = 'TIME FLIES LIKE AN ARROW'
    
        def on_next(info):
            label, (x, y), i = info
            label.move(x + i*12 + 15, y)
            print(len(scheduler._timers))
            label.show()
    
        def handle_label(label, i):
            delayer = ops.delay(i * 0.100)
            mapper = ops.map(lambda xy: (label, xy, i))
    
            return window.mousemove.pipe(
                delayer,
                mapper,
                )
    
        labeler = ops.flat_map_indexed(handle_label)
        mapper = ops.map(lambda c: QLabel(c, window))
    
        rx.from_(text).pipe(
            mapper,
            labeler,
        ).subscribe(on_next, on_error=print, scheduler=scheduler)
    
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/