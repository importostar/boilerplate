---
title: signals2 (1)
date: 2020-05-07
---
Example Python program signals2 (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout, QGroupBox, QDialog, QVBoxLayout, \
* from PyQt5.QtCore import pyqtSlot
* from DirListing import Listing

## Classes

* class ButtonTest(QDialog):

## Methods

* def __init__(self):
* def initUI(self):
* def createGridLayout(self):
* def on_click(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    
    import sys
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout, QGroupBox, QDialog, QVBoxLayout, \
        QGridLayout
    from PyQt5.QtCore import pyqtSlot
    
    from DirListing import Listing
    
    class ButtonTest(QDialog):
        def __init__(self):
            super(ButtonTest, self).__init__()
            self.top = 10
            self.left = 10
            self.width = 320
            self.height = 500
            self.initUI()
    
        def initUI(self):
            self.setWindowTitle("Directory Buttons")
            self.setGeometry(self.left, self.top, self.width, self.height)
            self.createGridLayout()
            windowLayout = QVBoxLayout()
            windowLayout.addWidget(self.horizontalGroupBox)
            self.setLayout(windowLayout)
            self.show()
    
        def createGridLayout(self):
            self.horizontalGroupBox = QGroupBox("Joe")
            layout = QGridLayout()
            counter = 0
    
            for obj in Listing:
                button = QPushButton(obj.filename)
                button.clicked.connect(self.on_click)
                button.setObjectName(obj.filename)
                layout.addWidget(button, counter, 0)
                counter = counter + 1
    
            self.horizontalGroupBox.setLayout(layout)
    
        @pyqtSlot()
        def on_click(self):
            print(self.sender().objectName())
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = ButtonTest()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
