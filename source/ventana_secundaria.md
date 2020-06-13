---
title: ventana_secundaria
date: 2020-05-07
---
Example Python program ventana_secundaria.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_ventana_secundaria(object):

## Methods

* def setupUi(self, ventana_secundaria):
* def retranslateUi(self, ventana_secundaria):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'ventana_secundaria.ui'
    #
    # Created by: PyQt5 UI code generator 5.10.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_ventana_secundaria(object):
        def setupUi(self, ventana_secundaria):
            ventana_secundaria.setObjectName("ventana_secundaria")
            ventana_secundaria.resize(568, 109)
            self.centralwidget = QtWidgets.QWidget(ventana_secundaria)
            self.centralwidget.setObjectName("centralwidget")
            self.etiqueta = QtWidgets.QLabel(self.centralwidget)
            self.etiqueta.setGeometry(QtCore.QRect(100, 20, 371, 41))
            font = QtGui.QFont()
            font.setPointSize(22)
            self.etiqueta.setFont(font)
            self.etiqueta.setObjectName("etiqueta")
            ventana_secundaria.setCentralWidget(self.centralwidget)
            self.statusbar = QtWidgets.QStatusBar(ventana_secundaria)
            self.statusbar.setObjectName("statusbar")
            ventana_secundaria.setStatusBar(self.statusbar)
    
            self.retranslateUi(ventana_secundaria)
            QtCore.QMetaObject.connectSlotsByName(ventana_secundaria)
    
        def retranslateUi(self, ventana_secundaria):
            _translate = QtCore.QCoreApplication.translate
            ventana_secundaria.setWindowTitle(_translate("ventana_secundaria", "Ventana Secundaria"))
            self.etiqueta.setText(_translate("ventana_secundaria", "Bienvenido a esta ventana"))
    
    
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        ventana_secundaria = QtWidgets.QMainWindow()
        ui = Ui_ventana_secundaria()
        ui.setupUi(ventana_secundaria)
        ventana_secundaria.show()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
