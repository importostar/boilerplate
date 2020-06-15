---
title: whySettingMultipleTimes
date: 2020-05-07
---
Example Python program whySettingMultipleTimes.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5 import QtCore, QtQml
* from PyQt5.QtWidgets import QApplication
* import QtQuick 2.7
* import QtQuick.Controls 1.4
* import CustomType 1.0

## Classes

* class CustomType(QtCore.QObject):

## Methods

* def __init__(self, parent = None):
* def names(self):
* def names(self, names):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5 import QtCore, QtQml
    from PyQt5.QtWidgets import QApplication
    
    
    class CustomType(QtCore.QObject):
        names_changed = QtCore.pyqtSignal()
    
        def __init__(self, parent = None):
            super().__init__(parent)
    
            self._names = []
            self._times_in_setter = 0
    
        @QtCore.pyqtProperty(QtCore.QVariant, notify = names_changed)
        def names(self):
            return self._names
        @names.setter
        def names(self, names):
            names_list = names.toVariant()
            # if names_list == self._names:
            #     return
            self._times_in_setter += 1
            self._names = names_list
            print(names)
            print("objectName: ", self.objectName())
            print("names: ", self._names)
            print("Times in setter: ", self._times_in_setter)
            print()
            self.names_changed.emit()
    
    
    QML = b"""
    import QtQuick 2.7
    import QtQuick.Controls 1.4
    
    import CustomType 1.0
    
    ApplicationWindow {
        visible: true
        width: 640
        height: 480
    
        Column {
            ComboBox {
                model: customType.names
            }
            ComboBox {
                model: customType2.names
            }
        }
    
        CustomType {
          id: customType
          objectName: "customType"
          names: ["one", "two"]
        }
        CustomType {
          id: customType2
          objectName: "customType2"
          names: customType.names
       }
    }
    """
    
    app = QApplication(sys.argv)
    QtQml.qmlRegisterType(CustomType, 'CustomType', 1, 0, 'CustomType')
    engine = QtQml.QQmlApplicationEngine()
    engine.loadData(QML)
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
