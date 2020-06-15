---
title: PyQt5_expro_expro_ui
date: 2020-05-07
---
Example Python program PyQt5_expro_expro_ui.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_Dialog(object):

## Methods

* def setupUi(self, Dialog):
* def retranslateUi(self, Dialog):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'pyqttest.ui'
    #
    # Created by: PyQt5 UI code generator 5.11.3
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(417, 550)
            self.lbl_display = QtWidgets.QLineEdit(Dialog)
            self.lbl_display.setGeometry(QtCore.QRect(11, 11, 391, 91))
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Fixed)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.lbl_display.sizePolicy().hasHeightForWidth())
            self.lbl_display.setSizePolicy(sizePolicy)
            self.lbl_display.setStyleSheet("background-color: rgb(183, 215, 255);\n"
    "font: 28pt \"Agency FB\";")
            self.lbl_display.setAlignment(QtCore.Qt.AlignRight|QtCore.Qt.AlignTrailing|QtCore.Qt.AlignVCenter)
            self.lbl_display.setObjectName("lbl_display")
            self.widget = QtWidgets.QWidget(Dialog)
            self.widget.setGeometry(QtCore.QRect(11, 119, 395, 421))
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.widget.sizePolicy().hasHeightForWidth())
            self.widget.setSizePolicy(sizePolicy)
            self.widget.setObjectName("widget")
            self.gridLayout = QtWidgets.QGridLayout(self.widget)
            self.gridLayout.setContentsMargins(0, 0, 0, 0)
            self.gridLayout.setObjectName("gridLayout")
            self.btn_7 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_7.sizePolicy().hasHeightForWidth())
            self.btn_7.setSizePolicy(sizePolicy)
            self.btn_7.setObjectName("btn_7")
            self.gridLayout.addWidget(self.btn_7, 0, 0, 1, 1)
            self.btn_8 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_8.sizePolicy().hasHeightForWidth())
            self.btn_8.setSizePolicy(sizePolicy)
            self.btn_8.setObjectName("btn_8")
            self.gridLayout.addWidget(self.btn_8, 0, 1, 1, 1)
            self.btn_9 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_9.sizePolicy().hasHeightForWidth())
            self.btn_9.setSizePolicy(sizePolicy)
            self.btn_9.setObjectName("btn_9")
            self.gridLayout.addWidget(self.btn_9, 0, 2, 1, 1)
            self.btn_plush = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_plush.sizePolicy().hasHeightForWidth())
            self.btn_plush.setSizePolicy(sizePolicy)
            self.btn_plush.setObjectName("btn_plush")
            self.gridLayout.addWidget(self.btn_plush, 0, 3, 1, 1)
            self.btn_4 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_4.sizePolicy().hasHeightForWidth())
            self.btn_4.setSizePolicy(sizePolicy)
            self.btn_4.setObjectName("btn_4")
            self.gridLayout.addWidget(self.btn_4, 1, 0, 1, 1)
            self.btn_5 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_5.sizePolicy().hasHeightForWidth())
            self.btn_5.setSizePolicy(sizePolicy)
            self.btn_5.setObjectName("btn_5")
            self.gridLayout.addWidget(self.btn_5, 1, 1, 1, 1)
            self.btn_6 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_6.sizePolicy().hasHeightForWidth())
            self.btn_6.setSizePolicy(sizePolicy)
            self.btn_6.setObjectName("btn_6")
            self.gridLayout.addWidget(self.btn_6, 1, 2, 1, 1)
            self.btn_sub = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_sub.sizePolicy().hasHeightForWidth())
            self.btn_sub.setSizePolicy(sizePolicy)
            self.btn_sub.setObjectName("btn_sub")
            self.gridLayout.addWidget(self.btn_sub, 1, 3, 1, 1)
            self.btn_1 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_1.sizePolicy().hasHeightForWidth())
            self.btn_1.setSizePolicy(sizePolicy)
            self.btn_1.setObjectName("btn_1")
            self.gridLayout.addWidget(self.btn_1, 2, 0, 1, 1)
            self.btn_2 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_2.sizePolicy().hasHeightForWidth())
            self.btn_2.setSizePolicy(sizePolicy)
            self.btn_2.setObjectName("btn_2")
            self.gridLayout.addWidget(self.btn_2, 2, 1, 1, 1)
            self.btn_3 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_3.sizePolicy().hasHeightForWidth())
            self.btn_3.setSizePolicy(sizePolicy)
            self.btn_3.setObjectName("btn_3")
            self.gridLayout.addWidget(self.btn_3, 2, 2, 1, 1)
            self.btn_mul = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_mul.sizePolicy().hasHeightForWidth())
            self.btn_mul.setSizePolicy(sizePolicy)
            self.btn_mul.setObjectName("btn_mul")
            self.gridLayout.addWidget(self.btn_mul, 2, 3, 1, 1)
            self.btn_clean = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_clean.sizePolicy().hasHeightForWidth())
            self.btn_clean.setSizePolicy(sizePolicy)
            self.btn_clean.setObjectName("btn_clean")
            self.gridLayout.addWidget(self.btn_clean, 3, 0, 1, 1)
            self.btn_0 = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_0.sizePolicy().hasHeightForWidth())
            self.btn_0.setSizePolicy(sizePolicy)
            self.btn_0.setObjectName("btn_0")
            self.gridLayout.addWidget(self.btn_0, 3, 1, 1, 1)
            self.btn_eq = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_eq.sizePolicy().hasHeightForWidth())
            self.btn_eq.setSizePolicy(sizePolicy)
            self.btn_eq.setObjectName("btn_eq")
            self.gridLayout.addWidget(self.btn_eq, 3, 2, 1, 1)
            self.btn_div = QtWidgets.QPushButton(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.btn_div.sizePolicy().hasHeightForWidth())
            self.btn_div.setSizePolicy(sizePolicy)
            self.btn_div.setObjectName("btn_div")
            self.gridLayout.addWidget(self.btn_div, 3, 3, 1, 1)
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Dialog"))
            self.lbl_display.setText(_translate("Dialog", "0"))
            self.btn_7.setText(_translate("Dialog", "7"))
            self.btn_8.setText(_translate("Dialog", "8"))
            self.btn_9.setText(_translate("Dialog", "9"))
            self.btn_plush.setText(_translate("Dialog", "+"))
            self.btn_4.setText(_translate("Dialog", "4"))
            self.btn_5.setText(_translate("Dialog", "5"))
            self.btn_6.setText(_translate("Dialog", "6"))
            self.btn_sub.setText(_translate("Dialog", "-"))
            self.btn_1.setText(_translate("Dialog", "1"))
            self.btn_2.setText(_translate("Dialog", "2"))
            self.btn_3.setText(_translate("Dialog", "3"))
            self.btn_mul.setText(_translate("Dialog", "*"))
            self.btn_clean.setText(_translate("Dialog", "C"))
            self.btn_0.setText(_translate("Dialog", "0"))
            self.btn_eq.setText(_translate("Dialog", "="))
            self.btn_div.setText(_translate("Dialog", "/"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
