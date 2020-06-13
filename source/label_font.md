---
title: label_font
date: 2020-05-07
---
Example Python program label_font.py
This program creates a PyQt GUI

## Modules

* from PyQt5.Qt import *
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_MainWindow(object):
* class Main(QMainWindow):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):
* 	def __init__(self):

## Code

Example Python PyQt program :

    from PyQt5.Qt import *
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5 import QtCore, QtGui, QtWidgets
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(466, 280)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(150, 30, 300, 300))
            self.font = QtGui.QFont()
            self.font.setPointSize(45)
            self.font.setBold(False)
            self.font.setWeight(50)
            self.label.setFont(self.font)
            self.label.setObjectName("label")
            MainWindow.setCentralWidget(self.centralwidget)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            self._translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(self._translate("MainWindow", "MainWindow"))
            self.label.setText(self._translate("MainWindow", "Label"))
    class Main(QMainWindow):
    	def __init__(self):
    		super(Main, self).__init__()
    		self.ui = Ui_MainWindow()
    		self.ui.setupUi(self)
    		self.ui.label.setText(self.ui._translate("MainWindow", "hello world"))
    		self.ui.font.setBold(True)
    		self.ui.label.setFont(self.ui.font)
    		#self.icon = QPixmap("3.jpg")
    		#self.ui.label.setPixmap(self.icon)
    		#self.ui.label.setScaledContents(1)
    		#self.ui.label.setMaximumSize(100,100)
    		#self.ui.label.setMinimumSize(100,100)
    if __name__ == "__main__":
        import sys
        app = QApplication(sys.argv)
        w = Main()
        w.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
