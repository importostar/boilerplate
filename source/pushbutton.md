---
title: pushbutton
date: 2020-05-07
---
Example Python program pushbutton.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout

## Classes

* class MyWidget(QWidget):

## Methods

* def __init__(self):
* def init_ui(self):
* def main():

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout
    
    
    class MyWidget(QWidget):
        def __init__(self):
            super().__init__()
            self.init_ui()
            
        def init_ui(self):
        	# create a button object
            btn = QPushButton("this is a button")
            
            # button click (press + release)
            btn.clicked.connect(lambda: print("this is a button clicked event!!"))
            
            # button press down
            btn.pressed.connect(lambda: print("this is a button pressed event!!"))
            
            # button press up
            btn.released.connect(lambda: print("this is a button released event!!"))
            
            # layout button
            hbox = QHBoxLayout()
            hbox.addWidget(btn)
            self.setLayout(hbox)
            self.setWindowTitle("test button")
            self.setGeometry(10, 10, 400, 500)
            self.show()
            
    
    def main():
        app = QApplication(sys.argv)
        widget = MyWidget()
        sys.exit(app.exec_())
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
