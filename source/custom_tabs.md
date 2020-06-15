---
title: custom_tabs
date: 2020-05-07
---
Example Python program custom_tabs.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import Qt
* from PyQt5.QtGui import QPixmap
* from PyQt5.QtWidgets import (QApplication, QDialog, QWidget,

## Classes

* class Dialog(QDialog):

## Methods

* def __init__(self):
* def createSignInForm(self):
* def createSignUpForm(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtCore import Qt
    from PyQt5.QtGui import QPixmap
    from PyQt5.QtWidgets import (QApplication, QDialog, QWidget,
                                 QLabel, QLineEdit, QHBoxLayout, QVBoxLayout, QPushButton, 
                                 QButtonGroup, QStackedLayout)
    
    
    class Dialog(QDialog):
    
        def __init__(self):
            super(Dialog, self).__init__()
            main_layout = QVBoxLayout()
            # image header
            img = QLabel()
            img.setPixmap(QPixmap('waves.png'))
            
            # custom tabs
            hbox = QHBoxLayout()
            self.new_project_button = QPushButton('Sign In')
            self.new_project_button.setObjectName('CustomTab')
            self.new_project_button.setCheckable(True)
            self.new_project_button.setChecked(True)    
            
            self.load_project_button = QPushButton('Register')
            self.load_project_button.setObjectName('CustomTab')
            self.load_project_button.setCheckable(True)
            
            # The button group box ensures exclusive tab selection
            self.group = QButtonGroup()
            self.group.addButton(self.new_project_button, 0)
            self.group.addButton(self.load_project_button, 1)
            hbox.addWidget(self.new_project_button)
            hbox.addWidget(self.load_project_button)
            hbox.setSpacing(0)
    
            # create stacked layout 
            self.stack = QStackedLayout()
            self.stack1 = QWidget()
            self.stack2 = QWidget()
            self.stack1.setContentsMargins(30, 0, 30, 0)
            self.stack2.setContentsMargins(30, 0, 30, 0)
            self.stack.addWidget(self.stack1)
            self.stack.addWidget(self.stack2)
            self.group.buttonClicked[int].connect(self.stack.setCurrentIndex)
    
            # Add content to stack layout  
            self.createSignInForm()
            self.createSignUpForm()
    
            main_layout.setContentsMargins(0,0,0,0)     
            main_layout.addWidget(img)
            main_layout.addLayout(hbox)
            main_layout.addLayout(self.stack)
            self.setLayout(main_layout)
    
            self.setWindowFlags(Qt.FramelessWindowHint)
            self.setMinimumSize(640, 480)
    
        def createSignInForm(self):
           
            layout = QVBoxLayout()
            layout.addStretch(1)
            layout.addWidget(QLabel("Username:"))
            textbox = QLineEdit()
            layout.addWidget(textbox)
            layout.addStretch(1)
    
            layout.addWidget(QLabel("Password:"))
            textbox = QLineEdit()
            textbox.setEchoMode(QLineEdit.Password)
            layout.addWidget(textbox)
            layout.addStretch(1)
            
            hbox = QHBoxLayout()
            button = QPushButton('Login')
            hbox.addWidget(button)
            hbox.addStretch(1)
            layout.addLayout(hbox)
            layout.addStretch(1)
    
            self.stack1.setLayout(layout)
    
        def createSignUpForm(self):
           
            layout = QVBoxLayout()
            layout.addStretch(1)
            layout.addWidget(QLabel("Email:"))
            textbox = QLineEdit()
            layout.addWidget(textbox)
            layout.addStretch(1)
    
            layout.addWidget(QLabel("Password:"))
            textbox = QLineEdit()
            textbox.setEchoMode(QLineEdit.Password)
            layout.addWidget(textbox)
            layout.addStretch(1)
            
            hbox = QHBoxLayout()
            button = QPushButton('Sign up')
            hbox.addWidget(button)
            hbox.addStretch(1)
            layout.addLayout(hbox)
            layout.addStretch(1)
    
            self.stack2.setLayout(layout)
    
    if __name__ == '__main__':
    
        style=''
        with open('style.qss', 'rt') as sytlesheet:
            style = sytlesheet.read()
    
        app = QApplication(sys.argv)
        app.setStyleSheet(style)
        dialog = Dialog()
    sys.exit(dialog.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
