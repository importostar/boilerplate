---
title: chat_summit_view_cl_chat
date: 2020-05-07
---
Example Python program chat_summit_view_cl_chat.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import *
* import sys

## Classes

* class Ui_MainWindow(object):
* class Mychat(QMainWindow, Ui_MainWindow):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):
* def __init__(self):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'cl_chat.ui'
    #
    # Created by: PyQt5 UI code generator 5.11.3
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtWidgets import *
    import sys
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
    
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(663, 450)
            MainWindow.setMinimumSize(QtCore.QSize(450, 450))
            MainWindow.setIconSize(QtCore.QSize(30, 30))
    
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
    
            self.gridLayout = QtWidgets.QGridLayout(self.centralwidget)
            self.gridLayout.setObjectName("gridLayout")
    
            self.openGLWidget = QtWidgets.QOpenGLWidget(self.centralwidget)
            self.openGLWidget.setObjectName("openGLWidget")
            self.gridLayout.addWidget(self.openGLWidget, 3, 3, 1, 1)
    
            self.verticalScrollBar_2 = QtWidgets.QScrollBar(self.centralwidget)
            self.verticalScrollBar_2.setOrientation(QtCore.Qt.Vertical)
            self.verticalScrollBar_2.setObjectName("verticalScrollBar_2")
            self.gridLayout.addWidget(self.verticalScrollBar_2, 0, 8, 1, 1)
    
            self.textEdit_2 = QtWidgets.QTextEdit(self.centralwidget)
            self.textEdit_2.setMaximumSize(QtCore.QSize(16777215, 111))
            self.textEdit_2.setAutoFillBackground(True)
            self.textEdit_2.setObjectName("textEdit_2")
            self.gridLayout.addWidget(self.textEdit_2, 3, 7, 1, 1)
    
            self.textBrowser = QtWidgets.QTextBrowser(self.centralwidget)
            self.textBrowser.setObjectName("textBrowser")
            self.gridLayout.addWidget(self.textBrowser, 0, 7, 1, 1)
    
            self.verticalScrollBar_3 = QtWidgets.QScrollBar(self.centralwidget)
            self.verticalScrollBar_3.setOrientation(QtCore.Qt.Vertical)
            self.verticalScrollBar_3.setObjectName("verticalScrollBar_3")
            self.gridLayout.addWidget(self.verticalScrollBar_3, 3, 8, 1, 1)
    
            self.textBrowser_3 = QtWidgets.QTextBrowser(self.centralwidget)
            self.textBrowser_3.setMinimumSize(QtCore.QSize(120, 0))
            self.textBrowser_3.setMaximumSize(QtCore.QSize(120, 16777215))
            self.textBrowser_3.setObjectName("textBrowser_3")
            self.gridLayout.addWidget(self.textBrowser_3, 0, 1, 4, 1)
    
            self.verticalWidget = QtWidgets.QWidget(self.centralwidget)
            self.verticalWidget.setMinimumSize(QtCore.QSize(75, 50))
            self.verticalWidget.setMaximumSize(QtCore.QSize(75, 16777215))
            self.verticalWidget.setAutoFillBackground(False)
            self.verticalWidget.setStyleSheet("QWidget{\n"
    "ackground-color =yellow; boder=2px}")
            self.verticalWidget.setObjectName("verticalWidget")
            self.verticalLayout = QtWidgets.QVBoxLayout(self.verticalWidget)
            self.verticalLayout.setObjectName("verticalLayout")
    
            self.label = QtWidgets.QLabel(self.verticalWidget)
            self.label.setMinimumSize(QtCore.QSize(50, 50))
            self.label.setBaseSize(QtCore.QSize(50, 50))
            self.label.setObjectName("label")
            self.verticalLayout.addWidget(self.label)
    
            self.label_2 = QtWidgets.QLabel(self.verticalWidget)
            self.label_2.setMinimumSize(QtCore.QSize(50, 50))
            self.label_2.setBaseSize(QtCore.QSize(50, 50))
            self.label_2.setObjectName("label_2")
            self.verticalLayout.addWidget(self.label_2)
            self.label_3 = QtWidgets.QLabel(self.verticalWidget)
            self.label_3.setMinimumSize(QtCore.QSize(50, 50))
            self.label_3.setBaseSize(QtCore.QSize(50, 50))
            self.label_3.setObjectName("label_3")
            self.verticalLayout.addWidget(self.label_3)
            self.label_4 = QtWidgets.QLabel(self.verticalWidget)
            self.label_4.setMinimumSize(QtCore.QSize(50, 50))
            self.label_4.setBaseSize(QtCore.QSize(50, 50))
            self.label_4.setObjectName("label_4")
            self.verticalLayout.addWidget(self.label_4)
            spacerItem = QtWidgets.QSpacerItem(20, 40, QtWidgets.QSizePolicy.Minimum, QtWidgets.QSizePolicy.Expanding)
            self.verticalLayout.addItem(spacerItem)
            self.pushButton = QtWidgets.QPushButton(self.verticalWidget)
            self.pushButton.setObjectName("pushButton")
            self.verticalLayout.addWidget(self.pushButton)
            self.gridLayout.addWidget(self.verticalWidget, 0, 0, 4, 1)
            self.verticalScrollBar_4 = QtWidgets.QScrollBar(self.centralwidget)
            self.verticalScrollBar_4.setOrientation(QtCore.Qt.Vertical)
            self.verticalScrollBar_4.setObjectName("verticalScrollBar_4")
            self.gridLayout.addWidget(self.verticalScrollBar_4, 0, 2, 4, 1)
            self.horizontalFrame = QtWidgets.QFrame(self.centralwidget)
            self.horizontalFrame.setObjectName("horizontalFrame")
            self.horizontalLayout = QtWidgets.QHBoxLayout(self.horizontalFrame)
            self.horizontalLayout.setObjectName("horizontalLayout")
            self.pushButton_9 = QtWidgets.QPushButton(self.horizontalFrame)
            self.pushButton_9.setObjectName("pushButton_9")
            self.horizontalLayout.addWidget(self.pushButton_9)
            self.pushButton_10 = QtWidgets.QPushButton(self.horizontalFrame)
            self.pushButton_10.setObjectName("pushButton_10")
            self.horizontalLayout.addWidget(self.pushButton_10)
            self.pushButton_11 = QtWidgets.QPushButton(self.horizontalFrame)
            self.pushButton_11.setObjectName("pushButton_11")
            self.horizontalLayout.addWidget(self.pushButton_11)
            spacerItem1 = QtWidgets.QSpacerItem(40, 20, QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Minimum)
            self.horizontalLayout.addItem(spacerItem1)
            self.pushButton_8 = QtWidgets.QPushButton(self.horizontalFrame)
            self.pushButton_8.setObjectName("pushButton_8")
            self.horizontalLayout.addWidget(self.pushButton_8)
            self.gridLayout.addWidget(self.horizontalFrame, 2, 7, 1, 1)
            MainWindow.setCentralWidget(self.centralwidget)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.label.setText(_translate("MainWindow", "photo"))
            self.label_2.setText(_translate("MainWindow", "chat"))
            self.label_3.setText(_translate("MainWindow", "friends"))
            self.label_4.setText(_translate("MainWindow", "function"))
            self.pushButton.setText(_translate("MainWindow", "PushButton"))
            self.pushButton_9.setText(_translate("MainWindow", "PushButton"))
            self.pushButton_10.setText(_translate("MainWindow", "PushButton"))
            self.pushButton_11.setText(_translate("MainWindow", "PushButton"))
            self.pushButton_8.setText(_translate("MainWindow", "PushButton"))
    
    class Mychat(QMainWindow, Ui_MainWindow):
    
        def __init__(self):
            super().__init__()
            self.setupUi(self)
    
    if __name__ == "__main__":
        app = QtWidgets.QApplication(sys.argv)
        window = Mychat()
        window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
