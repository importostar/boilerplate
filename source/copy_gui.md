---
title: copy_gui
date: 2020-05-07
---
Example Python program copy_gui.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import exercise
* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import  *
* from PyQt5.QtGui import *

## Classes

* class Labels(QMainWindow) :
* class new_Window(QWidget):

## Methods

* def __init__(self):
* def initUi(self) :
* def buttonClicked(self):
* def buttonClicked_2(self):
* def showDialog(self):
* def __init__(self):
* def window_screen(self):
* def setTableWidgetData(self):
* def button_cliked(self):

## Code

Example Python PyQt program :

    import exercise
    
    import sys
    
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import  *
    from PyQt5.QtGui import *
    
    
    class Labels(QMainWindow) :
    
        def __init__(self):
            super().__init__()
    
            self.initUi()
    
        def initUi(self) :
    
            self.setWindowTitle("라벨지 선택")
    
            label_button = QPushButton("여길 눌러주세요",self)
            label_button.move(70,50)
            label_button.resize(label_button.sizeHint())
            label_button.clicked.connect(self.buttonClicked)
    
            make_window_btn = QPushButton("윈도우 생성",self)
            make_window_btn.move(70,90)
            make_window_btn.resize(make_window_btn.sizeHint())
            make_window_btn.clicked.connect(self.buttonClicked_2)
            self.test = new_Window()
    
            openFile = QAction('Open', self)
            openFile.setShortcut('Ctrl + O')
            openFile.setStatusTip('Open new File')
            openFile.triggered.connect(self.showDialog)
    
            menubar = self.menuBar()
            fileMenu = menubar.addMenu('&File')
            fileMenu.addAction(openFile)
    
    
            self.setGeometry(300,300,400,300)
            self.show()
    
        def buttonClicked(self):
            self.showDialog()
    
        def buttonClicked_2(self):
            self.test.show()
    
    
    
            """
            pb = ProgressBar()
    
            for i in range(0, 100):
                time.sleep(0.05)
                pb.setValue(((i + 1) / 100) * 100)
                QApplication.processEvents()
    
            pb.close()
    
            QMessageBox.information(self, "Message", "Data Loaded")
            """
    
        def showDialog(self):
    
            fname = QFileDialog.getOpenFileName(self, 'file')
            print(fname[0])
    
    class new_Window(QWidget):
    
    
        def __init__(self):
            super().__init__()
    
            self.window_screen()
    
        def window_screen(self):
            self.setWindowTitle("Test")
            self.setGeometry(300,300,400,300)
            hbox = QHBoxLayout()
            #버튼
    
            self.button = QPushButton("호에엑")
            self.button.move(50,50)
            self.button.clicked.connect(self.button_cliked)
            hbox.addWidget(self.button)
    
            self.tableWidget = QTableWidget(self)
            self.tableWidget.resize(290,290)
            self.tableWidget.setRowCount(2)
            self.tableWidget.setColumnCount(2)
            hbox.addWidget(self.tableWidget)
            self.setTableWidgetData()
    
            # 레이블 생성
            self.lb = QLabel(self)
            hbox.addWidget(self.lb)
            self.setLayout(hbox)
    
    
        def setTableWidgetData(self):
            self.tableWidget.setItem(0,0,QTableWidgetItem("(0,0)"))
    
        def button_cliked(self):
            self.fname = QFileDialog.getOpenFileName(self, 'file')
            self.pixmap = QPixmap(self.fname[0])
            print(self.fname[0])
            height_label = 100
            self.lb.resize(self.width(), height_label)
            self.lb.setPixmap(self.pixmap.scaled(self.lb.size()))
    
    
    
    if __name__ == "__main__" :
        app = QApplication(sys.argv)
        lable = Labels()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
