---
title: iface
date: 2020-05-07
---
Example Python program iface.py

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
    
    # Form implementation generated from reading ui file 'interface.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.2
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(747, 649)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.textEdit = QtWidgets.QTextEdit(self.centralwidget)
            self.textEdit.setGeometry(QtCore.QRect(10, 30, 341, 301))
            self.textEdit.setStyleSheet("background: #FFFFE0;")
            self.textEdit.setObjectName("textEdit")
            self.textEdit_2 = QtWidgets.QTextEdit(self.centralwidget)
            self.textEdit_2.setGeometry(QtCore.QRect(370, 30, 361, 301))
            self.textEdit_2.setStyleSheet("background: #FFFFE0;")
            self.textEdit_2.setObjectName("textEdit_2")
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(10, 10, 301, 18))
            self.label.setStyleSheet("color: green;\n"
    " font-size: 12pt;")
            self.label.setObjectName("label")
            self.label_2 = QtWidgets.QLabel(self.centralwidget)
            self.label_2.setGeometry(QtCore.QRect(370, 10, 351, 18))
            self.label_2.setStyleSheet("color: green;\n"
    " font-size: 12pt;")
            self.label_2.setObjectName("label_2")
            self.pushButton = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton.setGeometry(QtCore.QRect(10, 480, 721, 41))
            self.pushButton.setStyleSheet("background: navy;\n"
    "color: white;\n"
    "font-size: 14pt")
            self.pushButton.setObjectName("pushButton")
            self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit.setGeometry(QtCore.QRect(10, 370, 721, 32))
            self.lineEdit.setObjectName("lineEdit")
            self.label_3 = QtWidgets.QLabel(self.centralwidget)
            self.label_3.setGeometry(QtCore.QRect(10, 340, 361, 18))
            self.label_3.setStyleSheet("color: green;\n"
    " font-size: 12pt;")
            self.label_3.setObjectName("label_3")
            self.comboBox = QtWidgets.QComboBox(self.centralwidget)
            self.comboBox.setGeometry(QtCore.QRect(10, 430, 341, 32))
            self.comboBox.setObjectName("comboBox")
            self.label_4 = QtWidgets.QLabel(self.centralwidget)
            self.label_4.setGeometry(QtCore.QRect(10, 410, 341, 18))
            self.label_4.setStyleSheet("color: green;\n"
    " font-size: 10pt;")
            self.label_4.setObjectName("label_4")
            self.comboBox_2 = QtWidgets.QComboBox(self.centralwidget)
            self.comboBox_2.setGeometry(QtCore.QRect(370, 430, 361, 32))
            self.comboBox_2.setObjectName("comboBox_2")
            self.label_5 = QtWidgets.QLabel(self.centralwidget)
            self.label_5.setGeometry(QtCore.QRect(370, 410, 341, 20))
            self.label_5.setStyleSheet("color: green;\n"
    " font-size: 10pt;")
            self.label_5.setObjectName("label_5")
            self.pushButton_2 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_2.setGeometry(QtCore.QRect(10, 540, 721, 51))
            self.pushButton_2.setStyleSheet("color: red;\n"
    "font-size: 14pt")
            self.pushButton_2.setObjectName("pushButton_2")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 747, 30))
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
            self.label.setText(_translate("MainWindow", "Текст для шифрования/расшифровки"))
            self.label_2.setText(_translate("MainWindow", "Зашифрованный (расшифрованный)текст"))
            self.pushButton.setText(_translate("MainWindow", "Зашифровать (расшифровать) текст!"))
            self.label_3.setText(_translate("MainWindow", "Пароль для шифрования/расшифровки:"))
            self.label_4.setText(_translate("MainWindow", "Выберите опцию (шифрование/расшифровка"))
            self.label_5.setText(_translate("MainWindow", "Выберите алгоритм шифрования/расшифровки"))
            self.pushButton_2.setText(_translate("MainWindow", "Очистить все поля"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
