---
title: reglade3
date: 2020-05-07
---
Example Python program reglade3.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QGridLayout, QMainWindow, QWidget, QApplication, QLineEdit, QLabel
* from PyQt5.QtGui import QIntValidator
* import sys

## Classes

* class MainWindow(QMainWindow):

## Methods

* def __init__(self, *args, **kwargs):   
* def setupUi(self):
* def textChanged(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QGridLayout, QMainWindow, QWidget, QApplication, QLineEdit, QLabel
    from PyQt5.QtGui import QIntValidator
    
    class MainWindow(QMainWindow):
        def __init__(self, *args, **kwargs):       
            super(MainWindow, self).__init__(*args, **kwargs) 
            self.setWindowTitle("Regla de 3") 
            self.setupUi()
    
        def setupUi(self):
            # === Widget contenedor para MainWindow
            self.centralwidget = QWidget(self)
            self.setCentralWidget(self.centralwidget)
            # === Campos de texto
            self.editA1 = QLineEdit()
            self.editA2 = QLineEdit()
            self.editB1 = QLineEdit()
            self.editB2 = QLineEdit()
            # === Validadores numéricos para los textos
            self.editA1.setValidator(QIntValidator())
            self.editA2.setValidator(QIntValidator())
            self.editB1.setValidator(QIntValidator())
            self.editB2.setReadOnly(True)
            self.editB2.setStyleSheet("background-color: lightgray")
            # === Grid Layout para posicionamiento
            self.gridLayout = QGridLayout()
            self.gridLayout.addWidget(self.editA1, 0, 0) 
            self.gridLayout.addWidget(QLabel("es a"),  0, 1) 
            self.gridLayout.addWidget(self.editA2, 0, 2) 
            self.gridLayout.addWidget(QLabel("como"),  1, 1) 
            self.gridLayout.addWidget(self.editB1, 2, 0) 
            self.gridLayout.addWidget(QLabel("es a"),  2, 1) 
            self.gridLayout.addWidget(self.editB2, 2, 2) 
            # === Configuración del layout en el widget contenedor
            self.centralwidget.setLayout(self.gridLayout)
            # === Configuracin de las señales
            self.editA1.textChanged.connect(self.textChanged)
            self.editA2.textChanged.connect(self.textChanged)
            self.editB1.textChanged.connect(self.textChanged)
            self.editB2.textChanged.connect(self.textChanged)
    
        def textChanged(self):
            try:
                valorA1 = float(self.editA1.text())
                valorA2 = float(self.editA2.text())
                valorB1 = float(self.editB1.text())
                self.editB2.setText(str(valorA2 * valorB1 / valorA1))
            except Exception as e:
                print(e)
            
    if __name__ == "__main__":    
        import sys
        app = QApplication(sys.argv)
        window = MainWindow()
        window.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
