---
title: ProcessStarter
date: 2020-05-07
---
Example Python program ProcessStarter.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* from PyQt5 import QtWidgets, QtCore, QtGui, QtTest
* from PyQt5 import QtWebEngine,QtWebEngineWidgets, QtWebEngineCore
* from PyQt5.QtWebEngineWidgets import QWebEngineView
* import os, subprocess, youtube_dl, MainWindow
* from MainWindow import *

## Classes

* class App(QMainWindow, Ui_MainWindow):

## Methods

* def __init__(self):
* def setUpStuff(self):
* #def event(self,obj):
* def getActualURL(self):
* def youtubeDownload(self):
* def setURLm(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    from PyQt5 import QtWidgets, QtCore, QtGui, QtTest
    from PyQt5 import QtWebEngine,QtWebEngineWidgets, QtWebEngineCore
    from PyQt5.QtWebEngineWidgets import QWebEngineView
    import os, subprocess, youtube_dl, MainWindow
    from MainWindow import *
    
    class App(QMainWindow, Ui_MainWindow):
        def __init__(self):
            super().__init__()
            self.setupUi(self)
            self.setUpStuff()
    
        def setUpStuff(self):
            #self.engineView = QWebEngineView
            #self.engineView.load(QWebEngineView, QtCore.QUrl("http://www.Youtube.com"))
            #self.webView.setEnabled(True)
            #self.webView.setObjectName("webView")
            #self.webView.setBaseSize(30, 30)
    
            self.webView = QWebEngineView()
            self.webView.load(QUrl('http://youtube.com'))
            self.webView.setBaseSize(500,500)
            self.webView.setVisible(True)
            self.getActualURL()
    
            self.gridLayout.addWidget(self.webView, 1, 0, 1, 2)
    
            #ui.downloadButton.setEnabled(False)
            #ui.setURL.setEnabled(False)
            self.downloadButton.clicked.connect(self.youtubeDownload)
            self.setURL.clicked.connect(self.setURLm)
            #self.getActualURL()
            #self.webView.installEventFilter(self)
    
        #def event(self,obj):
            #if obj == self.webView:
                #if(self.webView.hasFocus() == True):
                    #self.getActualURL()
                    #self.setURLm
    
            #return False
    
        def getActualURL(self):
            print("getactualurl")
            i = self.webView.url()
            i = str(i)
            i = i[19:]
            ilen = i.__len__()
            url = i[:ilen - 2]
            print(url)
            #self.urlInput.setText(url)
    
    
        @pyqtSlot()
        def youtubeDownload(self):
            print("ytdownload")
            try:
                with youtube_dl.YoutubeDL({}) as ydl:
                    login = os.getlogin()
                    path = "C:/Users/"+login+"/Downloads/Youtube_Downloader"
                    if not os.path.exists(path):
                        os.makedirs(path)
                    os.chdir(path)
                    ydl.download([str(self.urlInput.displayText())])
            except:
                msgBox = QMessageBox()
                msgBox.setText("Error:")
                msgBox.setInformativeText("An unknown error occurred. Ensure video link is correct")
                msgBox.setStandardButtons(QMessageBox.Ok)
                msgBox.setDefaultButton(QMessageBox.Ok)
                msgBox.exec_()
    
        @pyqtSlot()
        def setURLm(self):
            print("seturlm")
            try:
                url = self.urlInput.displayText()
                i7 = url[:7]
                i8 = url[:8]
                if (i7 == "http://" or i8 == "https://"):
                    pass
                else:
                    url = "http://"+url
                print(url)
    
                self.webView.load(QUrl(url))
            except:
                pass
    
    app = QApplication(sys.argv)
    l = App()
    l.show()
    
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
