---
title: qgeventdispatcher
date: 2020-05-07
---
Example Python program qgeventdispatcher.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import gevent.event
* from collections import defaultdict, deque
* from PyQt5.QtWidgets import QApplication, QPushButton
* from PyQt5.QtCore import QAbstractEventDispatcher, QTimer, QTimerEvent
* import itertools

## Classes

* class QGeventDispatcher(QAbstractEventDispatcher):

## Methods

* def __init__(self, *args):
* def _push_event(self, obj, evt):
* def _pop_events(self):
* def wakeUp(self):
* def flush(self):
* def interrupt(self):
* def hasPendingEvents(self):
* def processEvents(self, flags):
* def registeredTimers(self, obj):
* def registerTimer(self, tid, interval, ttype, obj):
* def unregisterTimer(self, tid):
* def unregisterTimers(self, obj):
* def registerSocketNotifier(self, *args):
* def unregisterSocketNotifier(self, *args):
* def main():
* def background():

## Code

Example Python PyQt program :

    import sys
    import gevent.event
    from collections import defaultdict, deque
    
    from PyQt5.QtWidgets import QApplication, QPushButton
    from PyQt5.QtCore import QAbstractEventDispatcher, QTimer, QTimerEvent
    
    
    class QGeventDispatcher(QAbstractEventDispatcher):
    
        # Init
    
        def __init__(self, *args):
            super(QGeventDispatcher, self).__init__(*args)
            self._awake = gevent.event.Event()
            self._timers = defaultdict(dict)
            self._events = deque()
    
        # Internals
    
        def _push_event(self, obj, evt):
            self._events.append((obj, evt))
            self._awake.set()
    
        def _pop_events(self):
            while self._events:
                yield self._events.popleft()
    
        # Control
    
        def wakeUp(self):
            self._awake.set()
            # Thread-safe notification
            self._awake.hub.loop.async().send()
    
        def flush(self):
            QApplication.sendPostedEvents()
            self._events.clear()
    
        def interrupt(self):
            self._awake.set()
    
        # Events
    
        def hasPendingEvents(self):
            return bool(self._events)
    
        def processEvents(self, flags):
            # First tick
            self.awake.emit()
            QApplication.sendPostedEvents()
            flags &= 0x1f
            print('Processing events (flag={})'.format(hex(int(flags))))
            # Waiting
            if int(flags) == 0x04:
                self.aboutToBlock.emit()
                self._awake.wait()
                self._awake.clear()
            else:
                raise NotImplemented
            # Fire events
            if not self._events:
                return False
            for obj, evt in self._pop_events():
                QApplication.sendEvent(obj, evt)
            return True
    
        # Timers
    
        def registeredTimers(self, obj):
            return self._timers[obj]
    
        def registerTimer(self, tid, interval, ttype, obj):
            event = QTimerEvent(tid)
            self._timers[obj][tid] = self.TimerInfo(tid, interval, ttype)
            gevent.spawn_later(interval / 1000., self._push_event, obj, event)
    
        def unregisterTimer(self, tid):
            return any(timer.pop(tid, None) for timer in self._timers.values())
    
        def unregisterTimers(self, obj):
            return bool(self._timers.pop(obj))
    
        # Sockets
    
        def registerSocketNotifier(self, *args):
            raise NotImplementedError
    
        def unregisterSocketNotifier(self, *args):
            raise NotImplementedError
    
    
    def main():
        QApplication.setEventDispatcher(QGeventDispatcher())
        # QApplication.setEventDispatcher(
        #     type('A', (QAbstractEventDispatcher,), {})())
        app = QApplication(sys.argv)
        print(app.eventDispatcher())
        w = QPushButton('Quit')
        w.clicked.connect(app.quit)
        w.resize(100, 50)
        w.setWindowTitle('Simple')
        w.show()
        QTimer.singleShot(5000, app.quit)
        sys.exit(app.exec_())
    
    
    def background():
        import itertools
        for x in itertools.count():
            print(x)
            gevent.sleep(1)
    
    
    if __name__ == '__main__':
        gevent.spawn(background)
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
