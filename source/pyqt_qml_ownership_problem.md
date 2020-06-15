---
title: pyqt_qml_ownership_problem
date: 2020-05-07
---
Example Python program pyqt_qml_ownership_problem.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* import signal
* from PyQt5.QtGui import QGuiApplication
* from PyQt5.QtQuick import QQuickView
* from PyQt5.QtCore import QUrl, QObject, QVariant, pyqtSlot
* from PyQt5.QtQml import QQmlEngine, qmlRegisterType

## Classes

* class Dummy(QObject):
* class GUIEntryPoint(QObject):

## Methods

* def __del__(self):
* def get_foo(self):
* def print_foo(self, foo):
* def run():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import os
    import sys
    import signal
    from PyQt5.QtGui import QGuiApplication
    from PyQt5.QtQuick import QQuickView
    from PyQt5.QtCore import QUrl, QObject, QVariant, pyqtSlot
    from PyQt5.QtQml import QQmlEngine, qmlRegisterType
    
    
    class Dummy(QObject):
    
        def __del__(self):
            print("Deleted")
    
    
    class GUIEntryPoint(QObject):
    
        @pyqtSlot(result=QVariant)
        def get_foo(self):
            foo = Dummy()
            print("Created {}".format(foo))
            print("Ownership after instantiation: {}".format(QQmlEngine.objectOwnership(foo)))
            #QQmlEngine.setObjectOwnership(foo, 1)  # has no effect
            return foo
    
        @pyqtSlot(QVariant)
        def print_foo(self, foo):
            print("{}, ownership: {}".format(foo, QQmlEngine.objectOwnership(foo)))
    
    
    def run():
        signal.signal(signal.SIGINT, signal.SIG_DFL)
    
        app = QGuiApplication(sys.argv)
    
        # these don't seem to make a difference
        qmlRegisterType(GUIEntryPoint, 'GUIEntryPoint', 1, 0, 'GUIEntryPoint')
        qmlRegisterType(Dummy, 'Dummy', 1, 0, 'Dummy')
    
        qml_url = QUrl.fromLocalFile(os.path.join('zzz.qml'))
        view = QQuickView()
    
        gep = GUIEntryPoint()
        view.rootContext().setContextProperty('BE', gep)
        view.setSource(qml_url)
    
        view.show()
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        run()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
