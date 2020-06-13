---
title: pyqt_test
date: 2020-05-07
---
Example Python program pyqt_test.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *
* import sys

## Classes

* class Form(QWidget):

## Methods

* def __init__(self, parent=None):
* def submitContact(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    
    class Form(QWidget):
        def __init__(self, parent=None):
            super(Form, self).__init__(parent)
    
            nameLabel = QLabel("Name:")
            self.nameLine = QLineEdit()
            self.submitButton = QPushButton("&Submit")
    
            buttonLayout1 = QVBoxLayout()
            buttonLayout1.addWidget(nameLabel)
            buttonLayout1.addWidget(self.nameLine)
            buttonLayout1.addWidget(self.submitButton)
    
            self.submitButton.clicked.connect(self.submitContact)
    
            mainLayout = QGridLayout()
            # mainLayout.addWidget(nameLabel, 0, 0)
            mainLayout.addLayout(buttonLayout1, 0, 1)
    
            self.setLayout(mainLayout)
            self.setWindowTitle("Hello Qt")
    
        def submitContact(self):
            name = self.nameLine.text()
    
            if name == "":
                QMessageBox.information(self, "Empty Field",
                                        "Please enter a name and address.")
                return
            else:
                QMessageBox.information(self, "Success!",
                                        "Hello %s!" % name)
    
    if __name__ == '__main__':
        import sys
    
        app = QApplication(sys.argv)
    
        screen = Form()
        screen.show()
    
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
