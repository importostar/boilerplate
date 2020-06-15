---
title: lme_ics_final_test (1)
date: 2020-05-07
---
Example Python program lme_ics_final_test (1).py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import picture_rc

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'test.ui'
    #
    # Created by: PyQt5 UI code generator 5.11.2
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(0, 0, 791, 561))
            self.label.setStyleSheet("border-image: url(:/figure/ics_game_cover.jpg);")
            self.label.setText("")
            self.label.setPixmap(QtGui.QPixmap(":/figure/ics_game_cover.jpg"))
            self.label.setScaledContents(True)
            self.label.setObjectName("label")
            self.pushButton = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton.setGeometry(QtCore.QRect(624, 392, 113, 32))
            self.pushButton.setObjectName("pushButton")
            self.pushButton_2 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_2.setGeometry(QtCore.QRect(626, 475, 113, 32))
            self.pushButton_2.setObjectName("pushButton_2")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 22))
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
            self.pushButton.setText(_translate("MainWindow", "play"))
            self.pushButton_2.setText(_translate("MainWindow", "exit"))
    
    import picture_rc
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
