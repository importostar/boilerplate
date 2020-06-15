---
title: pyqt_qml_gc_problem
date: 2020-05-07
---
Example Python program pyqt_qml_gc_problem.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function
* import os
* import sys
* import signal
* from random import randint
* from PyQt5.QtGui import QGuiApplication
* from PyQt5.QtQuick import QQuickView
* from PyQt5.QtCore import (Qt, QUrl, QObject, QVariant, QAbstractListModel,
* import sip
* from PyQt5.QtQml import QQmlEngine

## Classes

* class DummyObject(QObject):
* class DummyModel(QAbstractListModel):
* class GUIEntryPoint(QObject):

## Methods

* def transfer_ownership(obj):
* def transfer_ownership(obj):
* def transfer_ownership(obj):
* def item_getter():
* def something(self):
* def item_getter():
* def _setup_roles(self):
* def roleNames(self):
* def __init__(self, parent=None):
* def bye():
* def data(self, qindex, role):
* def rowCount(self, parent):
* def __del__(self):
* def get_model(self):
* def model_data_type(self):
* def run():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    from __future__ import print_function
    import os
    import sys
    import signal
    from random import randint
    from PyQt5.QtGui import QGuiApplication
    from PyQt5.QtQuick import QQuickView
    from PyQt5.QtCore import (Qt, QUrl, QObject, QVariant, QAbstractListModel,
                              pyqtSlot, pyqtProperty)
    
    
    # This code can be run on both Python 2 and 3
    #
    # This example demonstrates the problem where DummyModel gets garbage
    # collected by javascript. When the GUI button is pressed, you will see
    # that DummyModel's __del__ and destroyed signal get triggered.
    # After the model has been collected, listview will have missing items when
    # scrolled. Garbage collection can also be triggered by rapidly scrolling the
    # listview for about 10 seconds.
    #
    # By changing the two constants below you can try any combination of transfer
    # methods and types of model items, however all 4 of them behave the same (I'm
    # not considering the "nothing" transfer method) on the following setup:
    #    Qt 5.3.1 64-bit
    #    PyQt 5.3.2-snapshot-77bc10e785e2
    #    sip 4.16.3-snapshot-53f490fe8f52
    #    Ubuntu 14.04 64-bit
    #    Python 3.4.0 64-bit
    
    
    # change this to try out different ownership transfer methods
    TRANSFER_METHOD = 2  # 0 - nothing, 1 - sip.transferto, 2 - setObjectOwnership
    
    # change this to switch between model of integers and model of DummyObjects
    MODEL_DATA_TYPE = 1  # 0 - integers, 1 - DummyObjects
    
    
    if TRANSFER_METHOD == 0:
        print("\nWithout ownership transfer")
    
        def transfer_ownership(obj):
            pass
    
    elif TRANSFER_METHOD == 1:
        print("\nOwnership transfer using sip.transferto")
        import sip
    
        def transfer_ownership(obj):
            sip.transferto(obj, obj)
    
    elif TRANSFER_METHOD == 2:
        print("\nOwnership transfer using setObjectOwnership")
        from PyQt5.QtQml import QQmlEngine
    
        def transfer_ownership(obj):
            QQmlEngine.setObjectOwnership(obj, 1)
    
    else:
        assert False, "wrong TRANSFER_METHOD value"
    
    
    
    
    if MODEL_DATA_TYPE == 0:
        print("Model contains integers")
    
        def item_getter():
            return randint(1, 99)
    
    elif MODEL_DATA_TYPE == 1:
        print("Model contains DummyObjects")
    
        class DummyObject(QObject):
            @pyqtProperty(str, constant=True)
            def something(self):
                self._something = "item #{}".format(randint(1, 99))
                return self._something
    
        def item_getter():
            d = DummyObject()
            transfer_ownership(d)
            return d
    
    else:
        assert False, "wrong MODEL_DATA_TYPE value"
    
    
    
    class DummyModel(QAbstractListModel):
        ROLES = ("hello",)
        _ROLE_MAP = {}
    
        def _setup_roles(self):
            keys = range(Qt.UserRole + 1, Qt.UserRole + 1 + len(self.ROLES))
            self._ROLE_MAP = dict(zip(keys, self.ROLES))
    
        def roleNames(self):
            return self._ROLE_MAP
    
        def __init__(self, parent=None):
            super(DummyModel, self).__init__(parent)
            self._setup_roles()
    
            self._size = 20
    
            def bye():
                print("\n  DummyModel DESTROYED")
    
            self.destroyed.connect(bye)
    
        def data(self, qindex, role):
            i = qindex.row()
            # these three cases never happen, left them in just in case
            if not qindex.isValid():
                print("Invalid index, returning empty QVariant")
                return QVariant()
            if role not in self._ROLE_MAP:
                print("Invalid role, returning empty QVariant")
                return QVariant()
            if i < 0 or i > self._size:
                print("index {} out of bounds, returning empty QVariant".format(i))
                return QVariant()
    
            return item_getter()
    
        @pyqtSlot(result=int)
        def rowCount(self, parent):
            if parent.isValid():
                # this never happens
                raise RuntimeError("Model is a flat list, it can't have a parent")
            return self._size
    
        def __del__(self):
            print("\n  DummyModel DELETED")
    
    
    
    class GUIEntryPoint(QObject):
    
        @pyqtSlot(result=QVariant)
        def get_model(self):
            d = DummyModel()
            transfer_ownership(d)
            return d
    
        @pyqtProperty(int, constant=True)
        def model_data_type(self):
            return MODEL_DATA_TYPE
    
    
    
    app = None
    
    
    def run():
        global app
        signal.signal(signal.SIGINT, signal.SIG_DFL)
    
        app = QGuiApplication(sys.argv)
    
        qml_url = QUrl.fromLocalFile(os.path.join('ui.qml'))
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
