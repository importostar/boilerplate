---
title: io_core
date: 2020-05-07
---
Example Python program io_core.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *
* import sys

## Classes

* class Root(QMainWindow):

## Methods

* def __init__(self, QApp):
* def setupUi(self):
* def startUi(self):
* def updateUi(self):
* def updateUiQPB0(self):
* def updateUiQPB1(self):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    import sys
    
    class Root(QMainWindow):
        def __init__(self, QApp):
            super().__init__()
            self.QApp = QApp
        def setupUi(self):
            file = open('root.qss', 'r')
            self.PSQWRootStyle = file.read()
            file.close()
            del file
            self.setStyleSheet(self.PSQWRootStyle)
            self.PLQuestions = [['<b>1/6</b><hr><h1>時間割を確認しましたか？</h1>','ある','いらない'],
                                ['<b>2/6</b><hr><h1>教科書を入れましたか？</h1>','ある','いらない'],
                                ['<b>3/6</b><hr><h1>ノートを入れましたか？</h1>','ある','いらない'],
                                ['<b>4/6</b><hr><h1>給食の用意を入れましたか？</h1>','ある'],
                                ['<b>5/6</b><hr><h1>宿題を入れましたか？</h1>','ある','いらない'],
                                ['<b>6/6</b><hr><h1>筆箱を入れましたか？</h1>','ある','いらない']]
            self.PLQuestionCounter = 0
            self.setWindowTitle('教材チェック')
            self.showMaximized()
            self.QGLRoot = QGridLayout()
            self.QWTDummy = QWidget()
            self.setCentralWidget(self.QWTDummy)
            self.QWTDummy.setLayout(self.QGLRoot)
            self.QLBTool = QLabel(self)
            self.QLBTool.setText('Tool')
            self.QGLRoot.addWidget(self.QLBTool, 0, 0, 0, 2)
            self.QPB0 = QPushButton(self)
            self.QPB0.setText('0')
            self.QPB0.clicked.connect(self.updateUiQPB0)
            self.QGLRoot.addWidget(self.QPB0, 1, 0)
            self.QPB1 = QPushButton(self)
            self.QPB1.setText('ある')
            self.QPB1.clicked.connect(self.updateUiQPB1)
            self.QGLRoot.addWidget(self.QPB1, 1, 1)
        def startUi(self):
            self.show()
            self.updateUi()
        def updateUi(self):
            self.QLBTool.setText(self.PLQuestions[self.PLQuestionCounter][0])
            self.QPB0.setText(self.PLQuestions[self.PLQuestionCounter][1])
            self.QPB1.setText(self.PLQuestions[self.PLQuestionCounter][2])
        def updateUiQPB0(self):
            if self.PLQuestionCounter != len(self.PLQuestions) - 1:
                self.PLQuestionCounter += 1
            else:
                exit()
            self.updateUi()
        def updateUiQPB1(self):
            if self.PLQuestionCounter != len(self.PLQuestions) - 1:
                self.PLQuestionCounter += 1
            else:
                exit()
            self.updateUi()
    QApp = QApplication(sys.argv)
    
    App = Root(QApp)
    App.setupUi()
    App.startUi()
    
    sys.exit(QApp.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
