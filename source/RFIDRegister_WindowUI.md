---
title: RFIDRegister_WindowUI
date: 2020-05-07
---
Example Python program RFIDRegister_WindowUI.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'WindowUI.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.0
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(544, 876)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.tableView = QtWidgets.QTableView(self.centralwidget)
            self.tableView.setGeometry(QtCore.QRect(10, 90, 521, 651))
            self.tableView.setObjectName("tableView")
            self.tableView.horizontalHeader().setCascadingSectionResizes(True)
            self.tableView.horizontalHeader().setStretchLastSection(True)
            self.tableView.verticalHeader().setCascadingSectionResizes(True)
            self.tableView.verticalHeader().setStretchLastSection(False)
            self.rfidIDField = QtWidgets.QLineEdit(self.centralwidget)
            self.rfidIDField.setGeometry(QtCore.QRect(270, 20, 113, 20))
            self.rfidIDField.setObjectName("rfidIDField")
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(140, 20, 101, 21))
            font = QtGui.QFont()
            font.setFamily("Times New Roman")
            font.setPointSize(14)
            self.label.setFont(font)
            self.label.setObjectName("label")
            self.getEvents = QtWidgets.QPushButton(self.centralwidget)
            self.getEvents.setGeometry(QtCore.QRect(80, 50, 101, 31))
            font = QtGui.QFont()
            font.setFamily("Times New Roman")
            font.setPointSize(14)
            self.getEvents.setFont(font)
            self.getEvents.setObjectName("getEvents")
            self.goBack = QtWidgets.QPushButton(self.centralwidget)
            self.goBack.setGeometry(QtCore.QRect(190, 780, 181, 31))
            font = QtGui.QFont()
            font.setFamily("Times New Roman")
            font.setPointSize(14)
            self.goBack.setFont(font)
            self.goBack.setObjectName("goBack")
            self.deleteButton = QtWidgets.QPushButton(self.centralwidget)
            self.deleteButton.setGeometry(QtCore.QRect(360, 50, 101, 31))
            font = QtGui.QFont()
            font.setFamily("Times New Roman")
            font.setPointSize(14)
            self.deleteButton.setFont(font)
            self.deleteButton.setObjectName("deleteButton")
            self.insertButton = QtWidgets.QPushButton(self.centralwidget)
            self.insertButton.setGeometry(QtCore.QRect(220, 50, 101, 31))
            font = QtGui.QFont()
            font.setFamily("Times New Roman")
            font.setPointSize(14)
            self.insertButton.setFont(font)
            self.insertButton.setObjectName("insertButton")
            self.label_2 = QtWidgets.QLabel(self.centralwidget)
            self.label_2.setGeometry(QtCore.QRect(140, 750, 271, 21))
            font = QtGui.QFont()
            font.setFamily("Times New Roman")
            font.setPointSize(14)
            self.label_2.setFont(font)
            self.label_2.setText("")
            self.label_2.setAlignment(QtCore.Qt.AlignCenter)
            self.label_2.setObjectName("label_2")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 544, 21))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "RFID Register"))
            self.label.setText(_translate("MainWindow", "ID of marker"))
            self.getEvents.setText(_translate("MainWindow", "Get events"))
            self.goBack.setText(_translate("MainWindow", "Go back to marker list"))
            self.deleteButton.setText(_translate("MainWindow", "Delete"))
            self.insertButton.setText(_translate("MainWindow", "Insert"))
    
    
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        MainWindow = QtWidgets.QMainWindow()
        ui = Ui_MainWindow()
        ui.setupUi(MainWindow)
        MainWindow.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
