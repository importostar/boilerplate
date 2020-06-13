---
title: messages_between_widgets
date: 2020-05-07
---
Example Python program messages_between_widgets.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore
* from PyQt5.QtWidgets import QWidget, QLineEdit, QPushButton, QHBoxLayout, \
* import sys

## Classes

* class widgetB(QWidget):
* class widgetA(QWidget):
* class mainwindow(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def on_button_clicked(self):
* def on_procStart(self, message):
* def __init__(self, parent=None):
* def on_button_clicked(self):
* def on_widgetB_procDone(self, message):
* def __init__(self, parent=None):
* def on_button_clicked(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    #-*- coding:utf-8 -*-
    # Modified existing script for PyQt5 (https://stackoverflow.com/questions/14090353/)
    
    from PyQt5 import QtCore
    from PyQt5.QtWidgets import QWidget, QLineEdit, QPushButton, QHBoxLayout, \
        QMainWindow, QApplication
    
    class widgetB(QWidget):
        procDone = QtCore.pyqtSignal(str)
    
        def __init__(self, parent=None):
            super(widgetB, self).__init__(parent)
    
            self.lineEdit = QLineEdit(self)
            self.button = QPushButton("Send Message to A", self)
            self.layout = QHBoxLayout(self)
            self.layout.addWidget(self.lineEdit)
            self.layout.addWidget(self.button)
    
            self.button.clicked.connect(self.on_button_clicked)
    
        @QtCore.pyqtSlot()
        def on_button_clicked(self):
            self.procDone.emit(self.lineEdit.text())
    
        @QtCore.pyqtSlot(str)
        def on_procStart(self, message):
            self.lineEdit.setText("From A: " + message)
    
            self.raise_()
    
    class widgetA(QWidget):
        procStart = QtCore.pyqtSignal(str)
    
        def __init__(self, parent=None):
            super(widgetA, self).__init__(parent)
    
            self.lineEdit = QLineEdit(self)
            self.lineEdit.setText("Hello!")
    
            self.button = QPushButton("Send Message to B", self)
            self.button.clicked.connect(self.on_button_clicked)
    
            self.layout = QHBoxLayout(self)
            self.layout.addWidget(self.lineEdit)
            self.layout.addWidget(self.button)
    
        @QtCore.pyqtSlot()
        def on_button_clicked(self):
            self.procStart.emit(self.lineEdit.text())
    
        @QtCore.pyqtSlot(str)
        def on_widgetB_procDone(self, message):
            self.lineEdit.setText("From B: " + message)
    
            self.raise_()
    
    
    class mainwindow(QMainWindow):
        def __init__(self, parent=None):
            super(mainwindow, self).__init__(parent)
    
            self.button = QPushButton("Click Me", self)
            self.button.clicked.connect(self.on_button_clicked)
    
            self.setCentralWidget(self.button)
    
            self.widgetA = widgetA()
            self.widgetB = widgetB()
    
            self.widgetA.procStart.connect(self.widgetB.on_procStart)
            self.widgetB.procDone.connect(self.widgetA.on_widgetB_procDone)
    
        @QtCore.pyqtSlot()
        def on_button_clicked(self):
            self.widgetA.show()
            self.widgetB.show()
    
            self.widgetA.raise_()
    
    
    if __name__ == "__main__":
        import sys
    
        app  = QApplication(sys.argv)
        main = mainwindow()
        main.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
