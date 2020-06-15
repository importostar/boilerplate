---
title: PyQt5_Downloader
date: 2020-05-07
---
Example Python program PyQt5_Downloader.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtWidgets
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* from urllib.request import *
* import sys

## Classes

* class DownloaderApp(QtWidgets.QMainWindow):

## Methods

* def __init__(self, parent = None):
* def startDownload(self):
* def stylesheet(self):

## Code

Example Python PyQt program :

    from PyQt5 import QtWidgets
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    from urllib.request import *
    
    class DownloaderApp(QtWidgets.QMainWindow):
        def __init__(self, parent = None):
            super(DownloaderApp, self).__init__(parent)
            
            self.setObjectName("download")
            
            self.groupBox = QtWidgets.QGridLayout()
            self.groupBox.setObjectName("groupBox")
            
            self.resize(500, 150)
            
            self.progressBar = QtWidgets.QProgressBar()
            self.progressBar.setLayoutDirection(Qt.LeftToRight)
            self.progressBar.setProperty("value", 0)
            self.progressBar.setObjectName("progressBar")
            self.progressBar.setVisible(False)
            self.progressBar.setStyleSheet(stylesheet(self))
            
            self.plainTextEdit = QtWidgets.QLineEdit()
            self.plainTextEdit.setObjectName("plainTextEdit")
            self.plainTextEdit.text()==''
            
            self.pushButton = QtWidgets.QPushButton()
            self.pushButton.setCursor(QCursor(Qt.PointingHandCursor))
            self.pushButton.setObjectName("pushButton")
            self.pushButton.setFixedWidth(130)
            self.pushButton.setText("start Download")        
                   
            self.label = QtWidgets.QLabel()
            self.label.setObjectName("label")
            self.label.setText("URL:")
            
            self.statuslabel = QtWidgets.QLabel()
            self.statuslabel.setText("status")
            
            self.groupBox.addWidget(self.label, 0, 0 ) 
            self.groupBox.addWidget(self.plainTextEdit, 1, 0 , 1, 1)
            self.groupBox.addWidget(self.pushButton, 2, 0)
            self.groupBox.addWidget(self.progressBar, 3, 0, 1, 2)
            self.groupBox.addWidget(self.statuslabel, 4, 0, 1, 1 , Qt.AlignBottom)
            
            qw = QtWidgets.QWidget()
            qw.setLayout(self.groupBox)
            
            self.setCentralWidget(qw)
            
            self.setWindowTitle("Downloader")                
        
            self.pushButton.clicked.connect(self.startDownload)
            self.pushButton.clicked.connect(self.plainTextEdit.clear)
    
        def startDownload(self):
            if not self.plainTextEdit.text() or self.plainTextEdit.text()=='':
                    QMessageBox.information(myDownloader,"Warning","no link")
                    return
            self.progressBar.setVisible(True)
            QtWidgets.QApplication.processEvents(QEventLoop.AllEvents)
            enter=self.plainTextEdit.text()
            url=urlopen(enter)
            html=url.info()
            name = enter.split('/')[-1]
            name = QDir.homePath() + "/Downloads/" + name
            cl=html['Content-Length']
            f =open(name,'wb+')
            fl=0
            self.fl=0
            while 1:
                 QtWidgets.QApplication.processEvents(QEventLoop.AllEvents)
                 xr=url.read(1024)
                 fl+=len(xr)
                 self.progressBar.setValue(fl*100/int(cl))
                 QtWidgets.qApp.processEvents()
                 f.write(xr)
                 if not xr:break
                 del xr
                 QtWidgets.QApplication.processEvents(QEventLoop.AllEvents)
            f.close()
            QtWidgets.QMessageBox.information(myDownloader,"Message","Download complete")
            self.progressBar.setVisible(False)
            return
    
    def stylesheet(self):
        return """
    QProgressBar {
        border: 2px solid #D9D9D9;
        border-radius: 5px;
        text-align: center;
    }
    
    QProgressBar::chunk {
        background-color: #05B8CC;
        width: 20px;
    }
        """   
        
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        myDownloader = DownloaderApp()
        myDownloader.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
