---
title: sst
date: 2020-05-07
---
Example Python program sst.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import attr
* import PyQt5.QtCore
* import sys
* import time

## Classes

* class Timer:
* class O(PyQt5.QtCore.QObject):

## Methods

* def start(self):
* def stop(self):
* def dt(self):
* def dts(self):
* def __attrs_post_init__(self):
* def slot(self):
* def method(self):
* def main():

## Code

Example Python PyQt program :

    import attr
    import PyQt5.QtCore
    import sys
    import time
    
    
    @attr.s
    class Timer:
        _start_time = attr.ib(default=None)
        _stop_time = attr.ib(default=None)
        format = '{: 3.6f}'
    
        def start(self):
            self._stop_time = None
            self._start_time = time.monotonic()
    
        def stop(self):
            self._stop_time = time.monotonic()
    
        def dt(self):
            return self._stop_time - self._start_time
    
        def dts(self):
            return self.format.format(self.dt())
    
    
    @attr.s
    class O(PyQt5.QtCore.QObject):
        signal = PyQt5.QtCore.pyqtSignal()
        timer = attr.ib()
        _parent = attr.ib() #don't want as a actually property...
    
        def __attrs_post_init__(self):
            super().__init__(self._parent)
    
        @PyQt5.QtCore.pyqtSlot()
        def slot(self):
            self.timer.stop()
    
        def method(self):
            self.timer.stop()
    
    
    def main():
        app = PyQt5.QtCore.QCoreApplication(sys.argv)
    
        timer = Timer()
    
        auto_signal = O(timer=timer, parent=app)
        queued_signal = O(timer=timer, parent=app)
        method_signal = O(timer=timer, parent=app)
        slot = O(timer=timer, parent=app)
    
        auto_signal.signal.connect(slot.slot)
        queued_signal.signal.connect(slot.slot, PyQt5.QtCore.Qt.QueuedConnection)
        method_signal.signal.connect(slot.method)
    
        n = 1000000
    
        multiple_dt = 0
        for _ in range(n):
            timer.start()
            slot.slot()
            multiple_dt += timer.dt()
    
        print('{:>30s}'.format('direct: ') + timer.format.format(multiple_dt))
    
    
        multiple_dt = 0
        for _ in range(n):
            timer.start()
            auto_signal.signal.emit()
    
            multiple_dt += timer.dt()
    
        print('{:>30s}'.format('signal/slot: ') + timer.format.format(multiple_dt))
    
        multiple_dt = 0
        for _ in range(n):
            timer.start()
            queued_signal.signal.emit()
            app.processEvents()
    
            multiple_dt += timer.dt()
    
        print('{:>30s}'.format('queued signal/slot: ') + timer.format.format(multiple_dt))
    
        multiple_dt = 0
        for _ in range(n):
            timer.start()
            method_signal.signal.emit()
    
            multiple_dt += timer.dt()
    
        print(
            '{:>30s}'.format('method signal/slot: ') + timer.format.format(multiple_dt))
    
    
    if __name__ == '__main__':
        sys.exit(main())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
