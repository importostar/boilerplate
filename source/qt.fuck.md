---
title: qt.fuck
date: 2020-05-07
---
Example Python program qt.fuck.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton
* from PyQt5.QtWidgets import QLCDNumber, QLabel, QLineEdit
* from PyQt5 import QtGui

## Classes

* class Example(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def fuckit(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton
    from PyQt5.QtWidgets import QLCDNumber, QLabel, QLineEdit
    from PyQt5 import QtGui
    
    class Example(QWidget):
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            self.setGeometry(600, 600, 600, 600)
            self.setWindowTitle('Fuck you, Fucking Fuck!!!')
            self.btn  = QPushButton(self)
            self.btn.setText('Fuck it, boy!')
            self.btn.move(175, 300)
            self.lbl2 = QLabel(self)
            self.lbl2.setText("The number of times i fucked qt: 0")
            self.lbl2.setFixedWidth(250)
            self.lbl2.move(300, 300)
            self.lable = QLabel(self)
            self.lable.setText('FUCK QT!!!!')
            newfont = QtGui.QFont("Times", 48, QtGui.QFont.Bold)
            self.lable.setFont(newfont)
            self.lable.move(175, 200)
            self.fucked = 0
            self.btn.clicked.connect(self.fuckit)
    
        def fuckit(self):
            self.fucked += 1
            self.lbl2.setText(f'The number of times i fucked qt: {self.fucked}!')
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = Example()
        ex.show()
        sys.exit(app.exec())
        

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
