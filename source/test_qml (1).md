---
title: test_qml (1)
date: 2020-05-07
---
Example Python program test_qml (1).py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import Qt, QtCore, QtGui, QtQml, QtWidgets
* import QtQuick 2.0
* import QtQuick.Controls 1.4
* import QtTest 1.1
* import OutputType 1.0

## Classes

* class OutputType(QtCore.QObject):

## Methods

* def __init__(self, *args, **kwargs):
* def ChangeOutput(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    import sys
    
    from PyQt5 import Qt, QtCore, QtGui, QtQml, QtWidgets
    
    
    class OutputType(QtCore.QObject):
    
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            self.output = ""
    
        @QtCore.pyqtSlot()
        def ChangeOutput(self):
            self.output = "Hello"
    
    QML = b"""
    import QtQuick 2.0
    import QtQuick.Controls 1.4
    import QtTest 1.1
    
    import OutputType 1.0
    
    Item {
        width: 800
        height: 600
        visible: true
    
        OutputType {
            id: outputType
        }
    
        Text {
            id: txt
            text: outputType.output
        }
        Button {
            id: btn
            onClicked: {
                outputType.ChangeOutput()
            }
        }
        TestCase {
          name: "MouseTests"
          function test_clicked(){
              compare(txt.text, "")
              btn.clicked()
              compare(txt.text, "Hello")
          }
        }
    }
    """
    
    app = QtWidgets.QApplication(sys.argv + ["-nograb"])
    QtQml.qmlRegisterType(OutputType, 'OutputType', 1, 0, 'OutputType')
    engine = QtQml.QQmlApplicationEngine()
    engine.loadData(QML)
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
