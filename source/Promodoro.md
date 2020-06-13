---
title: Promodoro
date: 2020-05-07
---
Example Python program Promodoro.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget,QLabel, QMessageBox, QPushButton
* from PyQt5.QtGui import QIcon, QPixmap
* from PyQt5.QtCore import pyqtSlot, QTimer, QDateTime, QDate, QTime
* from Ui_Pomodoro import Ui_Dialog
* from PyQt5 import QtCore
* import time

## Classes

* class MyTimer(QWidget):

## Methods

* def __init__(self):
* def on_pushButtonStop_clicked(self):
* def on_pushButtonStart_clicked(self):
* def count_down(self):
* def msg(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import QApplication, QWidget,QLabel, QMessageBox, QPushButton
    from PyQt5.QtGui import QIcon, QPixmap
    from PyQt5.QtCore import pyqtSlot, QTimer, QDateTime, QDate, QTime
    from Ui_Pomodoro import Ui_Dialog
    from PyQt5 import QtCore
    import time
    
    
    
    
    
    class MyTimer(QWidget):
        def __init__(self):
            super().__init__()
    
            self.setGeometry(600,300,380,290)
            self.setFixedSize(self.size())
    
    
    
            # show image as bg
            label = QLabel(self)
            pixmap = QPixmap('promodoro.png')
            # pixmap = QPixmap('a3.jpg')
            label.setPixmap(pixmap)
            self.resize(pixmap.width(), pixmap.height())
    
            # call designer UI
            self.ui = Ui_Dialog()
            self.ui.setupUi(self)
    
            # how many chr in put into lcd
            self.ui.lcdNumber.setDigitCount(5) 
    
            # Create a timer
            self.timer = QTimer()
    
            # Connect the timer to the appropriate slot
            # this need to be at this level!
            self.timer.timeout.connect(self.count_down)
    
    
    
        @pyqtSlot()
        def on_pushButtonStop_clicked(self):
            self.timer.stop()
            self.min = 0
            self.sec = 0
            self.ui.lcdNumber.display(f"{str(self.min)}:{str(self.sec)}")
    
    
    
        @pyqtSlot()
        def on_pushButtonStart_clicked(self):
            # get sec value
            self.sec = self.ui.spinBoxSec.value()
            self.min = self.ui.spinBoxMin.value()
            self.ui.lcdNumber.display(f"{str(self.min)}:{str(self.sec)}")
            
    
            # Wait one second between slot calls
    
    
            self.timer.start(1000)
            
    
    
        def count_down(self):
            """ 
            it will count down the sec 
            it will decrease one min when sec hit 0
            it will stop when sec and min are both equal to 0
            
            """   
            self.ui.lcdNumber.display(f"{str(self.min)}:{str(self.sec)}")
            
            print(self.sec)
    
            if self.sec == 0 and self.min > 0:
                print('min minus one')
                self.min -= 1
                self.sec = 59
            elif self.sec == 0 and self.min == 0:
                print('stop timer')
                self.timer.stop()
                self.ui.spinBoxSec.setValue(0)
                self.ui.spinBoxMin.setValue(0)
                self.msg()
    
            else:
                self.sec = self.sec - 1
    
        
        def msg(self):
            reply = QMessageBox.information(self,                       
                                        "Time is Up",
                                        "Have a break!!",
                                        QMessageBox.Yes | QMessageBox.No)
    
    
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        win = MyTimer()
        win.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
