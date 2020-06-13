---
title: temperature_object
date: 2020-05-07
---
Example Python program temperature_object.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_Form(object):

## Methods

* def setupUi(self, Form):
* def retranslateUi(self, Form):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'temperatur.ui'
    #
    # Created by: PyQt5 UI code generator 5.4.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_Form(object):
        def setupUi(self, Form):
            Form.setObjectName("Form")
            Form.resize(260, 170)
            self.verticalLayoutWidget = QtWidgets.QWidget(Form)
            self.verticalLayoutWidget.setGeometry(QtCore.QRect(10, 10, 272, 151))
            self.verticalLayoutWidget.setObjectName("verticalLayoutWidget")
            self.verticalLayout = QtWidgets.QVBoxLayout(self.verticalLayoutWidget)
            self.verticalLayout.setSizeConstraint(QtWidgets.QLayout.SetMaximumSize)
            self.verticalLayout.setContentsMargins(0, 0, 0, 0)
            self.verticalLayout.setObjectName("verticalLayout")
            spacerItem = QtWidgets.QSpacerItem(20, 40, QtWidgets.QSizePolicy.Minimum, QtWidgets.QSizePolicy.Expanding)
            self.verticalLayout.addItem(spacerItem)
            self.horizontalLayout = QtWidgets.QHBoxLayout()
            self.horizontalLayout.setObjectName("horizontalLayout")
            spacerItem1 = QtWidgets.QSpacerItem(40, 20, QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Minimum)
            self.horizontalLayout.addItem(spacerItem1)
            self.cel_box = QtWidgets.QDoubleSpinBox(self.verticalLayoutWidget)
            self.cel_box.setAlignment(QtCore.Qt.AlignRight|QtCore.Qt.AlignTrailing|QtCore.Qt.AlignVCenter)
            self.cel_box.setDecimals(2)
            self.cel_box.setMinimum(-273.0)
            self.cel_box.setMaximum(100000000.0)
            self.cel_box.setProperty("value", 25.0)
            self.cel_box.setObjectName("cel_box")
            self.horizontalLayout.addWidget(self.cel_box)
            self.label = QtWidgets.QLabel(self.verticalLayoutWidget)
            self.label.setObjectName("label")
            self.horizontalLayout.addWidget(self.label)
            self.frn_box = QtWidgets.QDoubleSpinBox(self.verticalLayoutWidget)
            self.frn_box.setAlignment(QtCore.Qt.AlignRight|QtCore.Qt.AlignTrailing|QtCore.Qt.AlignVCenter)
            self.frn_box.setDecimals(2)
            self.frn_box.setMinimum(-495.4)
            self.frn_box.setMaximum(180000032.0)
            self.frn_box.setProperty("value", 77.0)
            self.frn_box.setObjectName("frn_box")
            self.horizontalLayout.addWidget(self.frn_box)
            spacerItem2 = QtWidgets.QSpacerItem(40, 20, QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Minimum)
            self.horizontalLayout.addItem(spacerItem2)
            self.verticalLayout.addLayout(self.horizontalLayout)
            spacerItem3 = QtWidgets.QSpacerItem(20, 40, QtWidgets.QSizePolicy.Minimum, QtWidgets.QSizePolicy.Expanding)
            self.verticalLayout.addItem(spacerItem3)
    
            self.retranslateUi(Form)
            self.cel_box.valueChanged['double'].connect(Form.convert_cel_to_frn)
            self.frn_box.valueChanged['double'].connect(Form.convert_frn_to_cel)
            QtCore.QMetaObject.connectSlotsByName(Form)
    
        def retranslateUi(self, Form):
            _translate = QtCore.QCoreApplication.translate
            Form.setWindowTitle(_translate("Form", "Form"))
            self.cel_box.setSuffix(_translate("Form", " C"))
            self.label.setText(_translate("Form", "<-->"))
            self.frn_box.setSuffix(_translate("Form", " F"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
