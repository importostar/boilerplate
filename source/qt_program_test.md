---
title: qt_program_test
date: 2020-05-07
---
Example Python program qt_program_test.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget, QPushButton, QHBoxLayout, QGroupBox, QDialog, QVBoxLayout
* from PyQt5.QtGui import QIcon
* from PyQt5.QtCore import pyqtSlot

## Classes

* class App(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def createHorizontalLayout(self):
* def on_click(self):
* def on_click2(self):

## Code

Example Python PyQt program :

    import sys
    import os
    from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget, QPushButton, QHBoxLayout, QGroupBox, QDialog, QVBoxLayout
    from PyQt5.QtGui import QIcon
    from PyQt5.QtCore import pyqtSlot
     
    
    class App(QWidget):
     
        def __init__(self):
            #here the 
            super().__init__()
            self.title = 'WINDOW_NAME_HERE'
            self.left = 10
            self.top = 10
            self.width = 640
            self.height = 480
            self.initUI()
            
            self.width1 = 100
            self.height2 = 100
     
        def initUI(self):
            self.setWindowTitle(self.title)
            self.setGeometry(self.left, self.top, self.width, self.height)
    
            self.createHorizontalLayout()
            windowLayout = QVBoxLayout()
            windowLayout.addWidget(self.horizontalGroupBox)
            self.setLayout(windowLayout)
        
            self.show()
        
        def createHorizontalLayout(self):
            self.horizontalGroupBox = QGroupBox()
            self.horizontalGroupBox.setTitle("What is your favorite color?")
            self.horizontalGroupBox.setMaximumHeight(200)
            self.horizontalGroupBox.setMaximumWidth(200)
            self.horizontalGroupBox.move(0,0)
        
            layout = QHBoxLayout()
            
            buttonBlue = QPushButton('Blue', self)
            buttonBlue.clicked.connect(self.on_click)
            layout.addWidget(buttonBlue) 
     
            buttonRed = QPushButton('Red', self)
            buttonRed.clicked.connect(self.on_click)
            layout.addWidget(buttonRed) 
     
            buttonGreen = QPushButton('Green', self)
            buttonGreen.clicked.connect(self.on_click)
            layout.addWidget(buttonGreen) 
     
            self.horizontalGroupBox.setLayout(layout)
    
        
        def on_click(self):
            print('PyQt5 button click')
        
        def on_click2(self):
            print('PyQt5 button click2')
     
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = App()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
