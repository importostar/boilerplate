---
title: joe_new
date: 2020-05-07
---
Example Python program joe_new.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import QSize
* from PyQt5.Qt import Qt
* from PyQt5.QtWidgets import QApplication, QMainWindow, QHBoxLayout, QPushButton, QLabel, QWidget

## Classes

* class MainWindow(QMainWindow):

## Methods

* def __init__(self):
* def set_statusbar_msg(self, msg):
* def build_ui(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtCore import QSize
    from PyQt5.Qt import Qt
    from PyQt5.QtWidgets import QApplication, QMainWindow, QHBoxLayout, QPushButton, QLabel, QWidget
    
    app = QApplication(sys.argv)
    
    qss="joe.qss"
    with open(qss,"r") as fh:
        app.setStyleSheet(fh.read())
    
    
    class MainWindow(QMainWindow):
        def __init__(self):
            super(MainWindow, self).__init__()
            self.resize(400, 500)
            self.setWindowTitle("Joe")
            self.setFixedSize(QSize(400, 500))
            self.set_statusbar_msg("Ready.")
            self.build_ui()
    
        def set_statusbar_msg(self, msg):
            self.statusBar().showMessage(msg)
    
        def build_ui(self):
            centralwidget = QWidget(self)
            MainWindow.setCentralWidget(self, centralwidget)
    
            utilsbox = QWidget(centralwidget)
            prognamelabel = QLabel(centralwidget)
            prognamelabel.setGeometry(25, 15, 325, 50)
            prognamelabel.setText("Joe Video Processor v0.1alpha")
            prognamelabel.setAlignment(Qt.AlignVCenter | Qt.AlignHCenter)
    
            utilsbox.setGeometry(25, 400, 325, 50)
            configbutton = QPushButton("Config")
            configbutton.setObjectName("blue")  # <<-------
            revertbutton = QPushButton("Revert")
            quitbutton = QPushButton("Quit")
            hbox = QHBoxLayout()
            utilsbox.setLayout(hbox)
            hbox.addWidget(configbutton, alignment=Qt.AlignVCenter | Qt.AlignHCenter)
            hbox.addWidget(revertbutton, alignment=Qt.AlignVCenter | Qt.AlignHCenter)
            hbox.addWidget(quitbutton, alignment=Qt.AlignVCenter | Qt.AlignHCenter)
            utilsbox.setParent(centralwidget)
    
    
    window = MainWindow()
    window.show()
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
