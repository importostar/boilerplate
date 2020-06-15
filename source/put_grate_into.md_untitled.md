---
title: put_grate_into_untitled
date: 2020-05-07
---
Example Python program put_grate_into.py_untitled.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import QAbstractItemView

## Classes

* class Ui_Dialog(object):

## Methods

* def setupUi(self, Dialog):
* def retranslateUi(self, Dialog):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'untitled.ui'
    #
    # Created by: PyQt5 UI code generator 5.11.3
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtWidgets import QAbstractItemView
    
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(1196, 712)
            self.pushButton = QtWidgets.QPushButton(Dialog)
            self.pushButton.setGeometry(QtCore.QRect(80, 30, 101, 31))
            self.pushButton.setObjectName("pushButton")
            self.pushButton_2 = QtWidgets.QPushButton(Dialog)
            self.pushButton_2.setGeometry(QtCore.QRect(690, 30, 81, 31))
            self.pushButton_2.setObjectName("pushButton_2")
            self.pushButton_3 = QtWidgets.QPushButton(Dialog)
            self.pushButton_3.setGeometry(QtCore.QRect(830, 30, 111, 31))
            self.pushButton_3.setObjectName("pushButton_3")
            self.pushButton_4 = QtWidgets.QPushButton(Dialog)
            self.pushButton_4.setGeometry(QtCore.QRect(520, 660, 101, 31))
            self.pushButton_4.setObjectName("pushButton_4")
            self.pushButton_5 = QtWidgets.QPushButton(Dialog)
            self.pushButton_5.setGeometry(QtCore.QRect(720, 660, 91, 31))
            self.pushButton_5.setObjectName("pushButton_5")
            self.pushButton_6 = QtWidgets.QPushButton(Dialog)
            self.pushButton_6.setGeometry(QtCore.QRect(966, 660, 91, 31))
            self.pushButton_6.setObjectName("pushButton_6")
            self.pushButton_7 = QtWidgets.QPushButton(Dialog)
            self.pushButton_7.setGeometry(QtCore.QRect(350, 660, 101, 31))
            self.pushButton_7.setObjectName("pushButton_7")
            self.comboBox = QtWidgets.QComboBox(Dialog)
            self.comboBox.setGeometry(QtCore.QRect(270, 30, 111, 31))
            self.comboBox.setObjectName("comboBox")
            self.comboBox_2 = QtWidgets.QComboBox(Dialog)
            self.comboBox_2.setGeometry(QtCore.QRect(400, 30, 251, 31))
            self.comboBox_2.setObjectName("comboBox_2")
            self.label_2 = QtWidgets.QLabel(Dialog)
            self.label_2.setGeometry(QtCore.QRect(110, 660, 151, 16))
            self.label_2.setObjectName("label_2")
            self.tableWidget = QtWidgets.QTableWidget(Dialog)
            self.tableWidget.setGeometry(QtCore.QRect(55, 91, 1111, 551))
            self.tableWidget.setObjectName("tableWidget")
            self.tableWidget.setColumnCount(0)
            self.tableWidget.setRowCount(0)
            self.tableWidget.setSelectionBehavior(QAbstractItemView.SelectRows )#设置表格的选取方式是行选取*
            self.tableWidget.setSelectionMode(QAbstractItemView.SingleSelection)#设置选取方式为单个选取*
            self.lineEdit = QtWidgets.QLineEdit(Dialog)
            self.lineEdit.setGeometry(QtCore.QRect(960, 30, 181, 31))
            self.lineEdit.setObjectName("lineEdit")
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
            Dialog.setTabOrder(self.pushButton, self.comboBox)
            Dialog.setTabOrder(self.comboBox, self.comboBox_2)
            Dialog.setTabOrder(self.comboBox_2, self.pushButton_2)
            Dialog.setTabOrder(self.pushButton_2, self.pushButton_3)
            Dialog.setTabOrder(self.pushButton_3, self.pushButton_7)
            Dialog.setTabOrder(self.pushButton_7, self.pushButton_4)
            Dialog.setTabOrder(self.pushButton_4, self.pushButton_5)
            Dialog.setTabOrder(self.pushButton_5, self.pushButton_6)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Dialog"))
            self.pushButton.setText(_translate("Dialog", "选择文件"))
            self.pushButton_2.setText(_translate("Dialog", "查询"))
            self.pushButton_3.setText(_translate("Dialog", "学号查找"))
            self.pushButton_4.setText(_translate("Dialog", "显示全部"))
            self.pushButton_5.setText(_translate("Dialog", "无成绩人员"))
            self.pushButton_6.setText(_translate("Dialog", "保存"))
            self.pushButton_7.setText(_translate("Dialog", "生成条形码"))
            self.label_2.setText(_translate("Dialog", "TextLabel"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
