---
title: maya_testUI_qt
date: 2020-05-07
---
Example Python program maya_testUI_qt.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtWidgets
* from PyQt5 import QtCore
* from PyQt5 import QtGui
* from maya import OpenMayaUI
* from sip import wrapinstance

## Classes

* class Test_UI(QtWidgets.QWidget):

## Methods

* def __init__(self, *args, **kwargs):
* def getMainWindow(self):
* def initUI(self):
* def menuAction(self):

## Code

Example Python PyQt program :

    from PyQt5 import QtWidgets
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    
    from maya import OpenMayaUI
    from sip import wrapinstance
    
    class Test_UI(QtWidgets.QWidget):
        
        def __init__(self, *args, **kwargs):
            
            super(Test_UI, self).__init__(*args, **kwargs)
            
            self.setParent(self.getMainWindow())
            self.setWindowFlags(QtCore.Qt.Window)
            
            self.setObjectName('Test_UI_uniqueId')
            self.setWindowTitle('Test User Interface')
            self.setGeometry(50, 50, 280, 150)
            self.initUI()
            
        def getMainWindow(self):
            
            ptr = OpenMayaUI.MQtUtil.mainWindow()
            mainWindow = wrapinstance(long(ptr), QtWidgets.QWidget)
            
            return mainWindow
            
        def initUI(self):
            
            self.layout = QtWidgets.QGridLayout(self)
            self.setLayout(self.layout)
            
            self.menuBar = QtWidgets.QMenuBar(parent = self.getMainWindow()) # requires parent
            self.menu = QtWidgets.QMenu(self)
            self.menu.setTitle("Menu")
            self.menuBar.addMenu(self.menu)
            self.menu.addAction("Menu Item")
            self.menu.triggered.connect(self.menuAction)
            
            self.text = QtWidgets.QLabel(self)
            self.text.setText("Test Window")
            self.text.setAlignment(QtCore.Qt.AlignCenter)
            
            self.layout.addWidget(self.menuBar, 0, 0, 1, 1)
            self.layout.addWidget(self.text, 0, 0, 1, 1)
            
        def menuAction(self):
            print("Menu Works.")
            
    Test_UI().show() # show UI

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
