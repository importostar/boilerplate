---
title: combobox
date: 2020-05-07
---
Example Python program combobox.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout
* from PyQt5.QtWidgets import QComboBox

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
    from PyQt5.QtWidgets import QComboBox
    
    
    class MyWidget(QWidget):
        def __init__(self):
            super().__init__()
            self.init_ui()
    
        def init_ui(self):
            # https://www.tutorialspoint.com/pyqt/pyqt_qcombobox_widget.htm
            
            # create combo box
            cbox = QComboBox()
            
            # add new items
            cbox.addItem("C++") # default item
            cbox.addItem("Java")
            cbox.addItem("Python")
            item = ["C", "Ruby", "JavaScript"]
            cbox.addItems(item)
            
            # get item index
            cbox.currentIndexChanged.connect(lambda index:
                                             print({
                                                 0: lambda: "select C++",
                                                 1: lambda: "select Java",
                                                 2: lambda: "select Python",
                                                 3: lambda: "select C",
                                                 4: lambda: "select Ruby",
                                                 5: lambda: "select JavaScript"
                                             }.get(index)()))
                                             
            # layout combo box
            hbox = QHBoxLayout()
            hbox.addWidget(cbox)
            self.setLayout(hbox)
            self.setWindowTitle("test ComboBox")
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
