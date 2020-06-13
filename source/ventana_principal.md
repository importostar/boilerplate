---
title: ventana_principal
date: 2020-05-07
---
Example Python program ventana_principal.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from ventana_secundaria import Ui_ventana_secundaria
* import sys

## Classes

* class Ui_ventana_principal(object):

## Methods

* def abrir_ventana(self):
* def setupUi(self, ventana_principal):
* def retranslateUi(self, ventana_principal):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'ventana_principal.ui'
    #
    # Created by: PyQt5 UI code generator 5.10.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from ventana_secundaria import Ui_ventana_secundaria
    
    class Ui_ventana_principal(object):
        
        def abrir_ventana(self):
            self.window = QtWidgets.QMainWindow()
            self.ui = Ui_ventana_secundaria()
            self.ui.setupUi(self.window)
            ventana_principal.hide()
            self.window.show()
            
        def setupUi(self, ventana_principal):
            ventana_principal.setObjectName("ventana_principal")
            ventana_principal.resize(371, 297)
            self.centralwidget = QtWidgets.QWidget(ventana_principal)
            self.centralwidget.setObjectName("centralwidget")
            self.boton_abrir = QtWidgets.QPushButton(self.centralwidget)
            self.boton_abrir.setGeometry(QtCore.QRect(110, 140, 141, 51))
            self.boton_abrir.setObjectName("boton_abrir")
            
            self.boton_abrir.clicked.connect(self.abrir_ventana)
            
    
            self.etiqueta = QtWidgets.QLabel(self.centralwidget)
            self.etiqueta.setGeometry(QtCore.QRect(40, 40, 291, 41))
            font = QtGui.QFont()
            font.setPointSize(16)
            self.etiqueta.setFont(font)
            self.etiqueta.setObjectName("etiqueta")
            ventana_principal.setCentralWidget(self.centralwidget)
            self.barra_de_estado = QtWidgets.QStatusBar(ventana_principal)
            self.barra_de_estado.setObjectName("barra_de_estado")
            ventana_principal.setStatusBar(self.barra_de_estado)
    
            self.retranslateUi(ventana_principal)
            QtCore.QMetaObject.connectSlotsByName(ventana_principal)
    
        def retranslateUi(self, ventana_principal):
            _translate = QtCore.QCoreApplication.translate
            ventana_principal.setWindowTitle(_translate("ventana_principal", "Ventana Principal"))
            self.boton_abrir.setText(_translate("ventana_principal", "Abrir Ventana"))
            self.etiqueta.setText(_translate("ventana_principal", "Haga clic para abrir la ventana"))
    
    
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        ventana_principal = QtWidgets.QMainWindow()
        ui = Ui_ventana_principal()
        ui.setupUi(ventana_principal)
        ventana_principal.show()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
