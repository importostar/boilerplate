---
title: ui_testchecked
date: 2020-05-07
---
Example Python program ui_testchecked.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_TestChecked(QtWidgets.QMainWindow):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'ui_testchecked.ui'
    #
    # Created by: PyQt5 UI code generator 5.6
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_TestChecked(QtWidgets.QMainWindow):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.itertable = QtWidgets.QTableWidget(self.centralwidget)
            self.itertable.setGeometry(QtCore.QRect(140, 90, 561, 321))
            self.itertable.setObjectName("itertable")
            self.itertable.setColumnCount(5)
            self.itertable.setRowCount(5)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setVerticalHeaderItem(0, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setVerticalHeaderItem(1, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setVerticalHeaderItem(2, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setVerticalHeaderItem(3, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setVerticalHeaderItem(4, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setHorizontalHeaderItem(0, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setHorizontalHeaderItem(1, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setHorizontalHeaderItem(2, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setHorizontalHeaderItem(3, item)
            item = QtWidgets.QTableWidgetItem()
            self.itertable.setHorizontalHeaderItem(4, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(0, 1, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(0, 3, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(1, 1, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(1, 3, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(2, 1, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(2, 3, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(3, 1, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(3, 3, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(4, 1, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.itertable.setItem(4, 3, item)
            self.iterbutton = QtWidgets.QPushButton(self.centralwidget)
            self.iterbutton.setGeometry(QtCore.QRect(350, 450, 151, 61))
            self.iterbutton.setObjectName("iterbutton")
            MainWindow.setCentralWidget(self.centralwidget)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            item = self.itertable.verticalHeaderItem(0)
            item.setText(_translate("MainWindow", "0"))
            item = self.itertable.verticalHeaderItem(1)
            item.setText(_translate("MainWindow", "1"))
            item = self.itertable.verticalHeaderItem(2)
            item.setText(_translate("MainWindow", "2"))
            item = self.itertable.verticalHeaderItem(3)
            item.setText(_translate("MainWindow", "3"))
            item = self.itertable.verticalHeaderItem(4)
            item.setText(_translate("MainWindow", "4"))
            item = self.itertable.horizontalHeaderItem(0)
            item.setText(_translate("MainWindow", "0"))
            item = self.itertable.horizontalHeaderItem(1)
            item.setText(_translate("MainWindow", "1"))
            item = self.itertable.horizontalHeaderItem(2)
            item.setText(_translate("MainWindow", "2"))
            item = self.itertable.horizontalHeaderItem(3)
            item.setText(_translate("MainWindow", "3"))
            item = self.itertable.horizontalHeaderItem(4)
            item.setText(_translate("MainWindow", "4"))
            __sortingEnabled = self.itertable.isSortingEnabled()
            self.itertable.setSortingEnabled(False)
            self.itertable.setSortingEnabled(__sortingEnabled)
            self.iterbutton.setText(_translate("MainWindow", "Table Iterate"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
