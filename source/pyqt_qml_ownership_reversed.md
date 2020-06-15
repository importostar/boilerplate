---
title: pyqt_qml_ownership_reversed
date: 2020-05-07
---
Example Python program pyqt_qml_ownership_reversed.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function
* import os
* import sys
* import signal
* from PyQt5.QtGui import QGuiApplication
* from PyQt5.QtQuick import QQuickView
* from PyQt5.QtCore import QUrl, QObject, pyqtProperty
* from PyQt5.QtQml import qmlRegisterType
* import sip

## Classes

* class Dummy(QObject):

## Methods

* def __init__(self, parent=None):
* def number(self):
* def __del__(self):
* def run():
* def quitting():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    # this code is runnable in both Python 2 and 3
    
    from __future__ import print_function
    import os
    import sys
    import signal
    from PyQt5.QtGui import QGuiApplication
    from PyQt5.QtQuick import QQuickView
    from PyQt5.QtCore import QUrl, QObject, pyqtProperty
    from PyQt5.QtQml import qmlRegisterType
    import sip
    
    
    class Dummy(QObject):
        counter = 0
    
        def __init__(self, parent=None):
            super(Dummy, self).__init__(parent)
            self._number = Dummy.counter
            Dummy.counter += 1
            print("Instantiated", self._number)
    
            # comment out this line and scroll the list to cause a segfault
            sip.transferto(self, self)
    
        @pyqtProperty(int, constant=True)
        def number(self):
            return self._number
    
        def __del__(self):
            print("Deleted", self._number)
    
    
    def run():
        signal.signal(signal.SIGINT, signal.SIG_DFL)
    
        app = QGuiApplication(sys.argv)
    
        qmlRegisterType(Dummy, 'Dummy', 1, 0, 'Dummy')
    
        qml_url = QUrl.fromLocalFile(os.path.join('zzz.qml'))
        view = QQuickView()
    
        view.setSource(qml_url)
    
        def quitting():
            print("\n\nquitting")
        app.aboutToQuit.connect(quitting)
    
        view.show()
    
        return_code = app.exec_()
        print("exited event loop")
        sys.exit(return_code)
        print("this never prints, as expected, however process remains running")
    
    
    if __name__ == '__main__':
        run()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
