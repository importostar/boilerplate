---
title: pyqt5_mppool (1)
date: 2020-05-07
---
Example Python program pyqt5_mppool (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import multiprocessing as mp
* from PyQt5.QtCore import QThread
* from PyQt5.QtWidgets import (QApplication, QMainWindow, QPushButton,

## Classes

* class Task(QThread):
* class Gui(QMainWindow):

## Methods

* def run(self):
* def mp_task(x):
* def __init__(self):
* def do_task(self):
* def main():

## Code

Example Python PyQt program :

    import sys
    import multiprocessing as mp
    
    from PyQt5.QtCore import QThread
    from PyQt5.QtWidgets import (QApplication, QMainWindow, QPushButton,
                                 QComboBox, QWidget, QVBoxLayout)
    
    
    class Task(QThread):
        def run(self):
            print('task started')
            with mp.Pool() as pool:
                res = pool.map(mp_task, range(10000))
            print('task finished')
    
    
    def mp_task(x):
        ret = 0
        for i in range(x + 50000):
            ret += i
        return ret
    
    
    class Gui(QMainWindow):
        def __init__(self):
            super().__init__()
            base = QWidget()
            layout = QVBoxLayout()
            button = QPushButton('click me')
            button.clicked.connect(self.do_task)
            combobox = QComboBox()
            combobox.addItems(['1', '2', '3', '4', '5'])
            layout.addWidget(button)
            layout.addWidget(combobox)
            base.setLayout(layout)
            self.setCentralWidget(base)
    
        def do_task(self):
            self.thread = Task()
            self.thread.start()
    
    
    def main():
        app = QApplication(sys.argv)
        window = Gui()
        window.show()
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
