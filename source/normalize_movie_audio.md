---
title: normalize_movie_audio
date: 2020-05-07
---
Example Python program normalize_movie_audio.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* import unicodedata
* from PyQt5.QtWidgets import QMainWindow, QApplication, QPushButton, QFileDialog, QLineEdit, QMessageBox, QComboBox, QPlainTextEdit, QProgressBar
* from PyQt5.QtGui import QIcon, QFont, QPalette, QBrush, QColor, QPen
* from PyQt5.QtCore import QSize, QEvent, QObject, QDir, QFileInfo, QProcess, Qt
* from gi.repository import GLib
* import pydub
* import subprocess

## Classes

* class QLineEditDropHandler(QObject):
* class App(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def eventFilter(self, obj, event):
* def __init__(self):
* def initUI(self):
* def closeEvent(self, event):
* def processOut(self):
* def dropEvent( self, event ):
* def text_changed(self):
* def make_lowder(self):
* def check_dBFS(self):
* def getFile(self):
* def msgbox(self, message):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    
    import sys
    import os
    import unicodedata
    from PyQt5.QtWidgets import QMainWindow, QApplication, QPushButton, QFileDialog, QLineEdit, QMessageBox, QComboBox, QPlainTextEdit, QProgressBar
    from PyQt5.QtGui import QIcon, QFont, QPalette, QBrush, QColor, QPen
    from PyQt5.QtCore import QSize, QEvent, QObject, QDir, QFileInfo, QProcess, Qt
    from gi.repository import GLib
    import pydub
    import subprocess
    
    class QLineEditDropHandler(QObject):
    
        def __init__(self, parent=None):
            QObject.__init__(self, parent)
    
        def eventFilter(self, obj, event):
            if event.type() == QEvent.DragEnter:
                event.accept()
            if event.type() == QEvent.Drop:
                md = event.mimeData()
                if md.hasUrls():
                    for url in md.urls():
                        obj.setText(url.path())
                        break
                event.accept()
            return QObject.eventFilter(self, obj, event)
    
    
    class App(QMainWindow):
    
        def __init__(self):
            super(QMainWindow, self).__init__()
            self.title = 'normalize audio in movie'
            self.initUI()
    
        def initUI(self):
            self.selectedFile = ""
            self.gain = "None"
            self.list = ["mp4", "mpeg", "ts", "flv", "avi", "3gp"]
            self.setWindowTitle(self.title)
            self.setFixedSize(600, 300)
            self.move(0, 0)
            self.setWindowIcon(QIcon.fromTheme("movie-editor"))
            self.setStyleSheet("font-family: Helvetica; background-color: qlineargradient(x1:0, y1:0, x1:2, y1:2, stop:0 #d3d7cf, stop:1 #babdb6);")
    
            self.process = QProcess(self)
            self.process.setProcessChannelMode(QProcess.MergedChannels)
            self.process.started.connect(lambda: self.statusBar().showMessage("running"), 0)
            self.process.finished.connect(lambda: self.statusBar().showMessage("finished!"), 0)
            self.process.finished.connect(lambda: self.bar.hide())
            self.process.readyRead.connect(self.processOut)
    
            self.textbox = QLineEdit(self)
            self.textbox.setStyleSheet("font-size: 8pt; padding-left: 2px;")
            self.textbox.textChanged.connect(self.text_changed)
            self.textbox.move(10, 10)
            self.textbox.resize(580, 26)
            self.textbox.setReadOnly(True)
            self.textbox.setPlaceholderText("drop file here or use 'Open'")
            self.textbox.installEventFilter(QLineEditDropHandler(self))
    
            self.selectbutton = QPushButton("Open", self)
            self.selectbutton.clicked.connect(self.getFile)
            self.selectbutton.setIcon(QIcon.fromTheme("document-open"))
            self.selectbutton.setStyleSheet("background-color: #729fcf; font-size: 8pt; padding-left: -12px;")
            self.selectbutton.resize(80, 22)
            self.selectbutton.move(10, 50)
    
            self.checkbutton = QPushButton("check max_dBFS", self)
            self.checkbutton.clicked.connect(self.check_dBFS)
            self.checkbutton.setIcon(QIcon.fromTheme("audio-x-generic"))
            self.checkbutton.setStyleSheet("background-color: #729fcf; font-size: 8pt; padding-left: -12px;")
            self.checkbutton.resize(130, 22)
            self.checkbutton.move(100, 50)
    
            self.makebutton = QPushButton("normalize", self)
            self.makebutton.clicked.connect(self.make_lowder)
            self.makebutton.setIcon(QIcon.fromTheme("player_play"))
            self.makebutton.setStyleSheet("background-color: #729fcf; font-size: 8pt; padding-left: -12px;")
            self.makebutton.resize(100, 22)
            self.makebutton.move(480, 50)
    
            self.outbox = QPlainTextEdit("output", self)
            self.outbox.setStyleSheet("background-color: #2e3436; color: #bedce9; font-size: 8pt; padding-left: 2px;")
            self.outbox.textChanged.connect(self.text_changed)
            self.outbox.move(10, 90)
            self.outbox.resize(580, 180)
            self.outbox.setReadOnly(True)
    
            self.statusBar().setStyleSheet("background-color: transparent; font-size: 8pt; color: #555753;")
            self.statusBar().showMessage("Ready", 0)
    
            self.bar = QProgressBar(self)
            self.bar.setRange(0,0)
            self.bar.setFixedWidth(80)
            self.bar.setFixedHeight(8)
            self.statusBar().addPermanentWidget(self.bar)
            self.bar.hide()
    
            self.show()
    
        def closeEvent(self, event):
            print("goodbye ...")
            event.accept()
    
        def processOut(self):
                try:
                    output = str(self.process.readAll(), encoding = 'utf8').rstrip()
                except Error:
                    output = str(self.process.readAll()).rstrip()          
                self.outbox.appendPlainText(output)
    
        def dropEvent( self, event ):
            data = event.mimeData()
            urls = data.urls()
            if ( urls and urls[0].scheme() == 'file' ):
                self.textbox.setText(urls)
    
        def text_changed(self):
            ext = self.textbox.text().rpartition(".")[-1]
            if ext in self.list:
                print("yes")
                print(self.textbox.text() + " loaded")
                self.selectedFile = self.textbox.text()
                self.statusBar().showMessage(self.textbox.text() + " loaded", 0)
            else:
                self.textbox.clear()
                print("no")
    
        def make_lowder(self):
            if self.gain == "None":
                self.check_dBFS()
            if not float(self.gain) < 0.1:
                extension = "." + QFileInfo(self.selectedFile).suffix()
                filename = QFileInfo(self.selectedFile).baseName()
                folder = QFileInfo(self.selectedFile).filePath().replace(filename, "").replace(extension, "")
                print("extension:", extension)
                print("filename:", filename)
                print("folder:", folder)
                videofolder = GLib.get_user_special_dir(GLib.USER_DIRECTORY_VIDEOS)
                outfile,_ = QFileDialog.getSaveFileName(self, "Select File", videofolder + "/" + filename + "_norm" + extension, ("Video Files (*" + extension + ")"))
                if outfile:
                    print(outfile)
                    self.outbox.clear()
                    cmd = 'ffmpeg -i "' + self.selectedFile + '" -y -vcodec copy -af "volume=' + self.gain + 'dB" "' + outfile.replace(".3gp", ".mp4") + '"'
                    print(cmd)
                    self.statusBar().showMessage("normalizing ....", 0)
                    self.bar.show()
                    self.process.start(cmd)
            else:
                print("enough gain")
    
        def check_dBFS(self):
            if not self.textbox.text() == "":
                self.statusBar().showMessage("checking .... big file needs more time ...", 0)
                sound = pydub.AudioSegment.from_file(self.selectedFile)
                max = str(sound.max_dBFS)[:4]
                self.statusBar().showMessage("max_dBFS: " + max, 0)
                self.gain = max.replace("-", "")
                print("apply gain:", self.gain)
            else:
                self.statusBar().showMessage("no File loaded!", 0)
    
        def getFile(self):
                videofolder = GLib.get_user_special_dir(GLib.USER_DIRECTORY_VIDEOS)
                dlg = QFileDialog()
                myfile,_ = dlg.getOpenFileName(self, "Select File", videofolder, ("Video Files (*.mp4 *.mpeg *.ts *.flv *.avi *.3gp)"))
                if myfile:
                    self.textbox.setText(myfile)
                    self.selectedFile = self.textbox.text()
    
        def msgbox(self, message):
            QMessageBox.warning(self, "Message", message)
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = App()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
