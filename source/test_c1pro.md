---
title: test_c1pro
date: 2020-05-07
---
Example Python program test_c1pro.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import cv2
* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *
* import PyQt5.QtGui as QtGui
* from PyQt5.QtGui import QImage, QPixmap
* import sys
* import time

## Classes

* class Thread(QThread):
* class App(QMainWindow):

## Methods

* def run(self):
* def close(self):
* def __init__(self):
* def setImage(self, image):
* def initUI(self):
* def closeEvent(self, a0: QtGui.QCloseEvent) -> None:

## Code

Example Python PyQt program :

    import cv2
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    import PyQt5.QtGui as QtGui
    from PyQt5.QtGui import QImage, QPixmap
    import sys
    import time
    
    class Thread(QThread):
        changePixmap = pyqtSignal(QImage)
    
        def run(self):
            self.shutdown_flag = False
    
            while not self.shutdown_flag:
                cap = cv2.VideoCapture(0)
                ret, frame = cap.read()
                print("new image")
                cap.release()
    
                if ret:
                    rgbImage = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
                    h, w, ch = rgbImage.shape
                    bytesPerLine = ch * w
                    convertToQtFormat = QtGui.QImage(rgbImage.data, w, h, bytesPerLine, QtGui.QImage.Format_RGB888)
                    p = convertToQtFormat.scaled(640, 480, Qt.KeepAspectRatio)
                    self.changePixmap.emit(p)
    
                time.sleep(5)
    
            print("closing thread")
            # cap.release()
    
    
        def close(self):
            self.shutdown_flag = True
    
    
    class App(QMainWindow):
        def __init__(self):
            super().__init__()
    
            self.initUI()
    
        @pyqtSlot(QImage)
        def setImage(self, image):
            self.label.setPixmap(QPixmap.fromImage(image))
    
        def initUI(self):
            self.setWindowTitle("test")
            # self.setGeometry(100,100,1000,1000)
            self.resize(1000, 1000)
            # create a label
            self.label = QLabel(self)
            self.label.move(280, 120)
            self.label.resize(640, 480)
            self.th = Thread(self)
            self.th.changePixmap.connect(self.setImage)
            self.th.start()
            self.show()
    
        def closeEvent(self, a0: QtGui.QCloseEvent) -> None:
            print("closing")
            self.th.close()
    
    
    if __name__ == '__main__':
    
        app = QApplication(sys.argv)
        ex = App()
        retVal = app.exec_()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
