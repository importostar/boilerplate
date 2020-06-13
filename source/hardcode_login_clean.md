---
title: hardcode_login_clean
date: 2020-05-07
---
Example Python program hardcode_login_clean.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtWidgets as qtw
* from PyQt5 import QtCore as qtc
* from PyQt5 import QtGui as qtg

## Classes

* class Mainwindow(qtw.QWidget):

## Methods

* def __init__(self, *args, **kwargs):

## Code

Example Python PyQt program :

    import sys
    from PyQt5 import QtWidgets as qtw
    from PyQt5 import QtCore as qtc
    from PyQt5 import QtGui as qtg
    
    
    class Mainwindow(qtw.QWidget):
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            # your code will go here
    
            # Input
            username_input = qtw.QLineEdit()
            password_input = qtw.QLineEdit()
            password_input.setEchoMode(qtw.QLineEdit.Password)
    
            # Pushbutton
            cancel_button = qtw.QPushButton("Cancel")
            login_button = qtw.QPushButton("Login")
    
    
            # Layout setzen alles reinpacken
            layout = qtw.QFormLayout()
    
            # Layout für input label
            layout.addRow("Username", username_input)
            layout.addRow("Password", password_input)
    
            # Layout für Button
            button_widget = qtw.QWidget()
            button_widget.setLayout(qtw.QHBoxLayout())
            button_widget.layout().addWidget(cancel_button)
            button_widget.layout().addWidget(login_button)
    
            # button layout zu allgemein layout hinzufügen
            layout.addRow(button_widget)
    
    
            self.setLayout(layout)
            # your code ends here
    
            self.show()
    
    
    if __name__ == '__main__':
        app = qtw.QApplication(sys.argv)
        w = Mainwindow()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
