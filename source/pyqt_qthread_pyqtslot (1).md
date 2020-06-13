---
title: pyqt_qthread_pyqtslot (1)
date: 2020-05-07
---
Example Python program pyqt_qthread_pyqtslot (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *
* from PyQt5 import QtCore 
* import sys

## Classes

* class TestThread(QThread):
* class TestGUI(QDialog):

## Methods

* def __init__(self, parent=None):
* def run(self):
* def __init__(self, parent=None):
* def threadStart(self):
* def threadStop(self):
* def threadEventHandler(self, n):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    from PyQt5 import QtCore 
    
    
    class TestThread(QThread):
    
        threadEvent = QtCore.pyqtSignal(int)
    
        def __init__(self, parent=None):
            super().__init__()
            self.n = 0
            self.main = parent
            self.isRun = False
    
        def run(self):
            while self.isRun:
                print('쓰레드 : ' + str(self.n))
    
                self.threadEvent.emit(self.n)
    
                self.n += 1
                self.sleep(1)
    
    
    class TestGUI(QDialog):
        def __init__(self, parent=None):
            super().__init__(parent)
    
            self.btn1 = QPushButton("쓰레드 시작", self)
            self.btn2 = QPushButton("쓰레드 정지", self)
    
            vertBox = QVBoxLayout()
            vertBox.addWidget(self.btn1)
            vertBox.addWidget(self.btn2)
            self.setLayout(vertBox)
            self.setGeometry(700, 500, 300, 100)
    
            self.btn1.clicked.connect(self.threadStart)
            self.btn2.clicked.connect(self.threadStop)
    
            self.show()
    
            # 쓰레드 인스턴스 생성
            self.th = TestThread(self)
    
            # 쓰레드 객체에 이벤트 바인딩
            self.th.threadEvent.connect(self.threadEventHandler)
    
        # @pyqtSlot()
        def threadStart(self):
            if not self.th.isRun:
                print('메인 : 쓰레드 시작')
                self.th.isRun = True
                self.th.start()
            else:
                print('이미 쓰레드가 생성되었습니다.')
    
        # @pyqtSlot()
        def threadStop(self):
            if self.th.isRun:
                print('메인 : 쓰레드 정지')
                self.th.isRun = False
    
        @pyqtSlot(int)
        def threadEventHandler(self, n):
            print('메인 : threadEvent(self,' + str(n) + ')')
    
    
    if __name__ == '__main__':
        import sys
    
        app = QApplication(sys.argv)
        form = TestGUI()
        app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
