---
title: process
date: 2020-05-07
---
Example Python program process.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from logging import getLogger
* from PyQt5.QtCore import QProcess, QTimer, pyqtSignal, pyqtProperty
* from sys import argv
* from PyQt5.QtCore import QCoreApplication

## Classes

* class Process(QProcess):

## Methods

* def __init__(self, timeout=1000, *args, **kwargs):
* def timedOut(self):
* def _timeout(self):
* def _started(self):
* def _finished(self, exitCode, exitStatus):
* def test():

## Code

Example Python PyQt program :

    from logging import getLogger
    
    from PyQt5.QtCore import QProcess, QTimer, pyqtSignal, pyqtProperty
    
    log = getLogger(__name__)
    
    
    class Process(QProcess):
        """Process class with built-in timeout
    
        Just a wrapper around QProcess with convenience signals succeeded and
        failed, and the ability to specify a timeout.
        """
    
        succeeded = pyqtSignal()
        failed = pyqtSignal()
    
        def __init__(self, timeout=1000, *args, **kwargs):
            super().__init__(*args, **kwargs)
    
            self.started.connect(self._started)
            self.finished.connect(self._finished)
    
            self._timer = QTimer()
            self._timer.setInterval(timeout)
            self._timer.timeout.connect(self._timeout)
    
            self._timedOut = False
    
        @pyqtProperty(bool)
        def timedOut(self):
            """Returns True if the process failed due to timing out"""
            return self._timedOut
    
        def _timeout(self):
            print('process timed out')
            self._timer.stop()
            self._timedOut = True
            self.kill()
    
        def _started(self):
            print('process started')
            self._timedOut = False
            self._timer.start()
    
        def _finished(self, exitCode, exitStatus):
            self._timer.stop()
    
            if exitStatus == QProcess.CrashExit or exitCode != 0:
                print('process failed')
                self.failed.emit()
            else:
                print('process succeeded')
                self.succeeded.emit()
    
    
    if __name__ == '__main__':
        from sys import argv
        from PyQt5.QtCore import QCoreApplication
    
        app = QCoreApplication(argv)
    
        def test():
            # Test the timeout functionality.
            process = Process(timeout=100)
            process.start('sleep 2')
            process.waitForFinished()
            app.quit()
    
        QTimer.singleShot(0, test)
    
        app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
