---
title: form (1)
date: 2020-05-07
---
Example Python program form (1).py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'ui_xml\calc.ui'
    #
    # Created by: PyQt5 UI code generator 5.8.2
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(340, 218)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.verticalLayout_2 = QtWidgets.QVBoxLayout(self.centralwidget)
            self.verticalLayout_2.setObjectName("verticalLayout_2")
            self.txt_res = QtWidgets.QLineEdit(self.centralwidget)
            self.txt_res.setObjectName("txt_res")
            self.verticalLayout_2.addWidget(self.txt_res)
            self.verticalLayout = QtWidgets.QVBoxLayout()
            self.verticalLayout.setObjectName("verticalLayout")
            self.gridLayout = QtWidgets.QGridLayout()
            self.gridLayout.setObjectName("gridLayout")
            self.btn_4 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_4.setObjectName("btn_4")
            self.gridLayout.addWidget(self.btn_4, 1, 0, 1, 1)
            self.btn_3 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_3.setObjectName("btn_3")
            self.gridLayout.addWidget(self.btn_3, 0, 2, 1, 1)
            self.btn_min = QtWidgets.QPushButton(self.centralwidget)
            self.btn_min.setObjectName("btn_min")
            self.gridLayout.addWidget(self.btn_min, 0, 3, 1, 1)
            self.btn_7 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_7.setObjectName("btn_7")
            self.gridLayout.addWidget(self.btn_7, 2, 0, 1, 1)
            self.btn_8 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_8.setObjectName("btn_8")
            self.gridLayout.addWidget(self.btn_8, 2, 1, 1, 1)
            self.btn_div = QtWidgets.QPushButton(self.centralwidget)
            self.btn_div.setObjectName("btn_div")
            self.gridLayout.addWidget(self.btn_div, 3, 3, 1, 1)
            self.btn_9 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_9.setObjectName("btn_9")
            self.gridLayout.addWidget(self.btn_9, 2, 2, 1, 1)
            self.btn_6 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_6.setObjectName("btn_6")
            self.gridLayout.addWidget(self.btn_6, 1, 2, 1, 1)
            self.btn_plu = QtWidgets.QPushButton(self.centralwidget)
            self.btn_plu.setObjectName("btn_plu")
            self.gridLayout.addWidget(self.btn_plu, 1, 3, 1, 1)
            self.btn_5 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_5.setObjectName("btn_5")
            self.gridLayout.addWidget(self.btn_5, 1, 1, 1, 1)
            self.btn_1 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_1.setObjectName("btn_1")
            self.gridLayout.addWidget(self.btn_1, 0, 0, 1, 1)
            self.btn_0 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_0.setObjectName("btn_0")
            self.gridLayout.addWidget(self.btn_0, 3, 0, 1, 1)
            self.btn_mul = QtWidgets.QPushButton(self.centralwidget)
            self.btn_mul.setObjectName("btn_mul")
            self.gridLayout.addWidget(self.btn_mul, 2, 3, 1, 1)
            self.btn_2 = QtWidgets.QPushButton(self.centralwidget)
            self.btn_2.setObjectName("btn_2")
            self.gridLayout.addWidget(self.btn_2, 0, 1, 1, 1)
            self.btn_eq = QtWidgets.QPushButton(self.centralwidget)
            self.btn_eq.setAutoDefault(True)
            self.btn_eq.setDefault(True)
            self.btn_eq.setFlat(False)
            self.btn_eq.setObjectName("btn_eq")
            self.gridLayout.addWidget(self.btn_eq, 3, 1, 1, 1)
            self.btn_cl = QtWidgets.QPushButton(self.centralwidget)
            self.btn_cl.setObjectName("btn_cl")
            self.gridLayout.addWidget(self.btn_cl, 3, 2, 1, 1)
            self.verticalLayout.addLayout(self.gridLayout)
            self.verticalLayout_2.addLayout(self.verticalLayout)
            MainWindow.setCentralWidget(self.centralwidget)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.btn_4.setText(_translate("MainWindow", "4"))
            self.btn_3.setText(_translate("MainWindow", "3"))
            self.btn_min.setText(_translate("MainWindow", "-"))
            self.btn_7.setText(_translate("MainWindow", "7"))
            self.btn_8.setText(_translate("MainWindow", "8"))
            self.btn_div.setText(_translate("MainWindow", "/"))
            self.btn_9.setText(_translate("MainWindow", "9"))
            self.btn_6.setText(_translate("MainWindow", "6"))
            self.btn_plu.setText(_translate("MainWindow", "+"))
            self.btn_5.setText(_translate("MainWindow", "5"))
            self.btn_1.setText(_translate("MainWindow", "1"))
            self.btn_0.setText(_translate("MainWindow", "0"))
            self.btn_mul.setText(_translate("MainWindow", "x"))
            self.btn_2.setText(_translate("MainWindow", "2"))
            self.btn_eq.setText(_translate("MainWindow", "="))
            self.btn_cl.setText(_translate("MainWindow", "Clear"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
