---
title: run_me
date: 2020-05-07
---
Example Python program run_me.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* import sip
* import signal
* from PyQt5.QtGui import QGuiApplication
* from PyQt5 import QtCore
* from PyQt5.QtCore import QUrl, Qt, QVariant, pyqtSlot, QAbstractListModel
* from PyQt5.QtQuick import QQuickView

## Classes

* class DummyModel(QAbstractListModel):

## Methods

* def _setup_roles(self):
* def roleNames(self):
* def __init__(self, model_size, parent=None):
* def data(self, qindex, role):
* def rowCount(self, parent):
* def run():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    # works correctly with SIP 4.16.6-snapshot-bf261aa4b322 and PyQt 5.4.1
    # causes the following error when run with SIP 4.16.9-snapshot-8dd533ab6ce9 and
    # PyQt 5.5-snapshot-6fd628724de4:
    #
    #    TypeError: invalid result type from DummyModel.roleNames()
    #
    # tried on Python 3.4 only
    
    import os
    import sys
    import sip
    import signal
    from PyQt5.QtGui import QGuiApplication
    from PyQt5 import QtCore
    from PyQt5.QtCore import QUrl, Qt, QVariant, pyqtSlot, QAbstractListModel
    from PyQt5.QtQuick import QQuickView
    
    
    class DummyModel(QAbstractListModel):
        ROLES = ("hello",)
        _ROLE_MAP = {}
    
        def _setup_roles(self):
            keys = range(Qt.UserRole + 1, Qt.UserRole + 1 + len(self.ROLES))
            self._ROLE_MAP = dict(zip(keys, self.ROLES))
    
        def roleNames(self):
            return self._ROLE_MAP
    
        def __init__(self, model_size, parent=None):
            QAbstractListModel.__init__(self, parent)
            self._setup_roles()
            self.model_size = model_size
    
        def data(self, qindex, role):
            if not qindex.isValid():
                print("Invalid index, returning empty QVariant")
                return QVariant()
            if role not in self._ROLE_MAP:
                print("Invalid role, returning empty QVariant")
                return QVariant()
    
            return "Item #{}".format(qindex.row())
    
        @pyqtSlot(result=int)
        def rowCount(self, parent):
            if parent.isValid():
                print("This shouldn't happen")
            return self.model_size
    
    
    def run():
        signal.signal(signal.SIGINT, signal.SIG_DFL)
    
        print("SIP version: {}".format(sip.SIP_VERSION_STR))
        print("PyQt version: {}".format(QtCore.PYQT_VERSION_STR))
    
        app = QGuiApplication(sys.argv)
        qml_url = QUrl.fromLocalFile(os.path.join('Application.qml'))
        gui_entrypoint = { 'model': DummyModel(80) }
        view = QQuickView()
        view.rootContext().setContextProperty('_BE', gui_entrypoint)
        view.setSource(qml_url)
    
        view.show()
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        run()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
