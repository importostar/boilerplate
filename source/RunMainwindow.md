---
title: RunMainwindow
date: 2020-05-07
---
Example Python program RunMainwindow.py
This program creates a PyQt GUI

## Modules

* import sys
* # import web
* from PyQt5.QtWidgets import  QApplication,QMainWindow
* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWebEngineWidgets import *
* # from PyQt5.QtWebEngineWidgets import *  

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    import sys
    # import web
    from PyQt5.QtWidgets import  QApplication,QMainWindow
    
    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'web.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.0
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtWebEngineWidgets import *
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.frame = QtWidgets.QFrame(self.centralwidget)
            self.frame.setGeometry(QtCore.QRect(72, 110, 461, 96))
            self.frame.setFrameShape(QtWidgets.QFrame.StyledPanel)
            self.frame.setFrameShadow(QtWidgets.QFrame.Raised)
            self.frame.setObjectName("frame")
            self.gridLayout = QtWidgets.QGridLayout(self.frame)
            self.gridLayout.setObjectName("gridLayout")
            self.pushButton = QtWidgets.QPushButton(self.frame)
            self.pushButton.setObjectName("pushButton")
            self.gridLayout.addWidget(self.pushButton, 0, 0, 1, 1)
            self.pushButton_2 = QtWidgets.QPushButton(self.frame)
            self.pushButton_2.setObjectName("pushButton_2")
            self.gridLayout.addWidget(self.pushButton_2, 0, 1, 1, 1)
            self.pushButton_3 = QtWidgets.QPushButton(self.frame)
            self.pushButton_3.setObjectName("pushButton_3")
            self.gridLayout.addWidget(self.pushButton_3, 0, 2, 1, 1)
            self.lineEdit = QtWidgets.QLineEdit(self.frame)
            self.lineEdit.setObjectName("lineEdit")
            self.gridLayout.addWidget(self.lineEdit, 1, 0, 1, 2)
            self.lineEdit_2 = QtWidgets.QLineEdit(self.frame)
            self.lineEdit_2.setObjectName("lineEdit_2")
            self.gridLayout.addWidget(self.lineEdit_2, 1, 2, 1, 1)
            self.gridFrame = QtWidgets.QFrame(self.centralwidget)
            self.gridFrame.setGeometry(QtCore.QRect(100, 300, 160, 80))
            self.gridFrame.setObjectName("gridFrame")
            self.gridLayout_2 = QtWidgets.QGridLayout(self.gridFrame)
            self.gridLayout_2.setObjectName("gridLayout_2")
            self.webEngineView = QWebEngineView(self.centralwidget)
            self.webEngineView.setGeometry(QtCore.QRect(420, 250, 361, 271))
            self.webEngineView.setUrl(QtCore.QUrl("https://music.163.com/"))
            self.webEngineView.setObjectName("webEngineView")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 30))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.pushButton.setText(_translate("MainWindow", "PushButton"))
            self.pushButton_2.setText(_translate("MainWindow", "PushButton"))
            self.pushButton_3.setText(_translate("MainWindow", "PushButton"))
    # from PyQt5.QtWebEngineWidgets import *  
    
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        mainWindow = QMainWindow()
        ui = Ui_MainWindow()
        #  向主窗口上添加控件
        ui.setupUi(mainWindow)
        mainWindow.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
