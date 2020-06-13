---
title: AudioConverter
date: 2020-05-07
---
Example Python program AudioConverter.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import (QAbstractListModel, QDir, QFile,
* from PyQt5.QtWidgets import (QApplication, QGridLayout, QMenu, QAction, 
* from PyQt5.QtGui import QIcon
* from PyQt5.Qt import QKeySequence, QSizePolicy
* import os, subprocess
* import encodings
* #import platform ### replace comment for Windows or OSX
* import pydub
* from PyQt5.QtCore import (QAbstractListModel, QDir, QFile,
* from PyQt5.QtWidgets import (QApplication, QGridLayout, QMenu, QAction, 
* from PyQt5.QtGui import QIcon
* from PyQt5.Qt import QKeySequence, QSizePolicy
* import os, subprocess
* import encodings
* #import platform ### replace comment for Windows or OSX
* import pydub
* import sys

## Classes

* class Window(QMainWindow):
* class Window(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def __init__(self, parent=None):
* def keyPressEvent(self, event):
* def deleteSelectedRow(self):
* def check_ffmpeg(self, name):
* def make_ogg(self):
* def make_mp3(self):
* def open_folder(self, path):
* def fillTable(self, path):
* def selectedRow(self):
* def selectFirstRow(self):
* def loadDir(self):
* def updateStatus(self, number):
* def createStatusBar(self):
* def msgbox(self, message): 
* def closeEvent(self, event):
* def handleQuit(self):
* def myStyleSheet(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    ########################################################
    from PyQt5.QtCore import (QAbstractListModel, QDir, QFile,
                                                        QModelIndex, Qt, QItemSelectionModel)
    from PyQt5.QtWidgets import (QApplication, QGridLayout, QMenu, QAction, 
                                                                QTableWidget, QTableWidgetItem, QWidget, QPushButton, QFileDialog, QMainWindow, 
                                                                QMessageBox, QAbstractItemView, QComboBox, QLabel, QSpacerItem)
    from PyQt5.QtGui import QIcon
    from PyQt5.Qt import QKeySequence, QSizePolicy
    import os, subprocess
    import encodings
    #import platform ### replace comment for Windows or OSX
    import pydub
    
    class Window(QMainWindow):
        def __init__(self, parent=None):
            super(Window, self).__init__(parent)
    
            self.songlist = []
            self.infolder = ""
            self.outfolder = ""
    
            self.setStyleSheet(myStyleSheet(self))
    
            ### buttons & combo boxes
    #!/usr/bin/python3
    ########################################################
    from PyQt5.QtCore import (QAbstractListModel, QDir, QFile,
                                                        QModelIndex, Qt, QItemSelectionModel)
    from PyQt5.QtWidgets import (QApplication, QGridLayout, QMenu, QAction, 
                                                                QTableWidget, QTableWidgetItem, QWidget, QPushButton, QFileDialog, QMainWindow, 
                                                                QMessageBox, QAbstractItemView, QComboBox, QLabel, QSpacerItem)
    from PyQt5.QtGui import QIcon
    from PyQt5.Qt import QKeySequence, QSizePolicy
    import os, subprocess
    import encodings
    #import platform ### replace comment for Windows or OSX
    import pydub
    
    class Window(QMainWindow):
        def __init__(self, parent=None):
            super(Window, self).__init__(parent)
    
            self.songlist = []
            self.infolder = ""
            self.outfolder = ""
    
            self.setStyleSheet(myStyleSheet(self))
    
            ### buttons & combo boxes
            btnLoad = QPushButton("select Folder")
            btnLoad.setIcon(QIcon.fromTheme("folder"))
            btnLoad.setFixedWidth(130)
            btnLoad.clicked.connect(self.loadDir)
    
            btn_mp3 = QPushButton("convert to mp3")
            btn_mp3.setIcon(QIcon.fromTheme("audio-x-generic"))
    #        btn_mp3.setFixedWidth(130)
            btn_mp3.clicked.connect(self.make_mp3)
    
            btn_ogg = QPushButton("convert to ogg")
            btn_ogg.setIcon(QIcon.fromTheme("audio-x-generic"))
    #        btn_ogg.setFixedWidth(130)
            btn_ogg.clicked.connect(self.make_ogg)
    
            self.comboBitrate_mp3 = QComboBox()
            self.comboBitrate_mp3.setFixedWidth(130)
            self.comboBitrate_mp3.addItem("96")
            self.comboBitrate_mp3.addItem("128")
            self.comboBitrate_mp3.addItem("192")
            self.comboBitrate_mp3.addItem("256")
            self.comboBitrate_mp3.addItem("320")
    
            self.comboBitrate_ogg = QComboBox()
            self.comboBitrate_ogg.setFixedWidth(130)
            self.comboBitrate_ogg.addItem("45")
            self.comboBitrate_ogg.addItem("64")
            self.comboBitrate_ogg.addItem("80")
            self.comboBitrate_ogg.addItem("96")
            self.comboBitrate_ogg.addItem("112")
            self.comboBitrate_ogg.addItem("128")
            self.comboBitrate_ogg.addItem("192")
    
            lbl_mp3 = QLabel("kBit/s")
            lbl_mp3.setFixedWidth(44)
    
            lbl_ogg = QLabel("kBit/s")
            lbl_ogg.setFixedWidth(44)
    
            self.view = QTableWidget()
            self.view.setToolTip("delete entry with 'delete' key")
            self.view.setSelectionBehavior(QAbstractItemView.SelectRows)
            self.view.setSelectionMode(QAbstractItemView.SingleSelection)
            self.view.setEditTriggers(QAbstractItemView.NoEditTriggers)
            self.view.verticalHeader().setVisible(False)
            self.view.horizontalHeader().setVisible(False)
            self.view.horizontalHeader().setStretchLastSection(True)
            self.view.setColumnCount(1)
    
            ### layout
            layout = QGridLayout()
    
            layout.addWidget(self.view, 0, 0, 1, 6)
            layout.addWidget(btnLoad, 1, 0)
            layout.addWidget(self.comboBitrate_mp3, 1, 1)
            layout.addWidget(lbl_mp3, 1, 2)
            layout.addWidget(self.comboBitrate_ogg, 1, 3)
            layout.addWidget(lbl_ogg, 1, 4)
            layout.addWidget(btn_mp3, 2, 1)
            layout.addWidget(btn_ogg, 2, 3)
    
            myWidget = QWidget()
            myWidget.setLayout(layout)
    
            self.setCentralWidget(myWidget)
    
            self.setWindowTitle("Audio Converter * convert to mp3 or ogg")
            self.setWindowIcon(QIcon.fromTheme("audio-x-generic"))
            self.setMinimumSize(520, 200)
            self.setGeometry(0,0,550,400)
    
            self.createStatusBar()
            self.view.setFocus()
            self.comboBitrate_mp3.setCurrentIndex(2)
            self.comboBitrate_ogg.setCurrentIndex(3)
    
        def keyPressEvent(self, event):
            self.view.setFocus()
            print(event.key())
            if event.key() == Qt.Key_Delete:
                self.deleteSelectedRow()
            else:
                event.accept()
    
        def deleteSelectedRow(self):
            row = self.selectedRow()
            self.view.removeRow(row)
            del self.songlist[row]
            print("Row " + str(row) + " deleted")
            self.view.selectRow(row)
    
        def check_ffmpeg(self, name):
            try:
                devnull = open(os.devnull)
                subprocess.Popen([name], stdout=devnull, stderr=devnull).communicate()
            except OSError as e:
                if e.errno == os.errno.ENOENT:
                    return False
            return True
    
        def make_ogg(self):
            if self.songlist == []:
                QMessageBox.warning(self, "Error", "no files in list!")
            else:
                quality = self.comboBitrate_ogg.currentText()
                dir = QDir(self.infolder)
                print(dir.absolutePath())
                if dir.mkpath("ogg_" + quality):
                    self.outfolder = self.infolder + "/ogg_" + quality
                    print("%s%s%s" % ("dir ", "ogg_" + quality, " created"))
                    i = 0
                    self.view.selectRow(i)
                    if self.songlist == []:
                        QMessageBox.warning(self, "Error", "no files in list!")
                    else:
                        for song in self.songlist:
                            base=os.path.basename(self.infolder + song)
                            oldsong = os.path.splitext(base)[0]
                            targetsong = self.infolder + song
                            newsong = self.outfolder + "/" + oldsong + ".ogg"
                            self.statusBar().showMessage("converting " + song, 0 )
                            sound = pydub.AudioSegment.from_file(targetsong)
                            sound.export(newsong, "ogg", codec="libvorbis", parameters=["-aq", "0", "-ar", quality + "000"])
                            i = i + 1
                            self.view.selectRow(i)
                        self.statusBar().showMessage("Finished!", 0)
                        self.open_folder(self.outfolder)
                else:
                    print("%s%s%s" % ("cannot create", "dir", self.outfolder))
    
        def make_mp3(self):
            if self.songlist == []:
                QMessageBox.warning(self, "Error", "no files in list!")
            else:
                dir = QDir(self.infolder)
                print(dir.absolutePath())
                if dir.mkpath("mp3_" + self.comboBitrate_mp3.currentText()):
                    self.outfolder = self.infolder + "/mp3_" + self.comboBitrate_mp3.currentText()
                    print("%s%s%s" % ("dir ", "mp3_" + self.comboBitrate_mp3.currentText(), " created"))
                    i = 0
                    self.view.selectRow(i)
                    if self.songlist == []:
                        QMessageBox.warning(self, "Error", "no files in list!")
                    else:
                        for song in self.songlist:
                            base=os.path.basename(self.infolder + song)
                            oldsong = os.path.splitext(base)[0]
                            targetsong = self.infolder + song
                            newsong = self.outfolder + "/" + oldsong + ".mp3"
                            self.statusBar().showMessage("converting " + song, 0 )
                            sound = pydub.AudioSegment.from_file(targetsong)
                            sound.export(newsong, format="mp3", bitrate=self.comboBitrate_mp3.currentText())
                            i = i + 1
                            self.view.selectRow(i)
                        self.statusBar().showMessage("Finished!", 0)
                        self.open_folder(self.outfolder)
                else:
                    print("%s%s%s" % ("cannot create", "dir", self.outfolder))
    
         ### replace comments for Windows or OSX
        def open_folder(self, path):
    #        if platform.system() == "Windows":
    #            os.startfile(path)
    #        elif platform.system() == "Darwin":
    #            subprocess.Popen(["open", path])
    #        else:
                subprocess.Popen(["xdg-open", path])
    
        def fillTable(self, path):
            self.view.clear()
            self.dir = QDir(path)
            self.infolder = path + "/"
            mlist = []
            mlist.append("*.flac")
            mlist.append("*.wav")
            mlist.append("*.m4a")
            mlist.append("*.ogg")
            mlist.append("*.mp3")
            mlist.append("*.mp4")
            self.fileList = self.dir.entryList(mlist, QDir.Files, QDir.IgnoreCase)
            for f in self.fileList:
                self.view.insertRow(self.view.rowCount())
                mf = QTableWidgetItem(str(f))
                self.view.setItem(self.view.rowCount() - 1, 0, mf)
                self.songlist.append(f)
            self.view.resizeRowsToContents()
            if self.view.rowCount() > 0:
                self.updateStatus(self.view.rowCount())
    
        def selectedRow(self):
            if self.view.selectionModel().hasSelection():
                row =  self.view.selectionModel().selectedIndexes()[0].row()
                return int(row)
    
        def selectFirstRow(self):
            self.view.selectRow(0)
    
        def loadDir(self):
            dlg = QFileDialog()
            dlg.setFileMode(QFileDialog.Directory)
            fileName = dlg.getExistingDirectory(self, "select Directory", "", QFileDialog.ShowDirsOnly  | QFileDialog.DontResolveSymlinks)
            if fileName:
                self.infolder = fileName
                self.fillTable(fileName)
    
        def updateStatus(self, number):
            self.statusBar().showMessage("loaded %d files" % number)
            self.selectFirstRow()
    
        def createStatusBar(self):
            self.statusBar().showMessage("Welcome to Audio Converter Linux", 0)
    
        def msgbox(self, message): 
            QMessageBox.warning(self, "Message", message)
    
        def closeEvent(self, event):
            return
    
        def handleQuit(self):
            quit()
    
    def myStyleSheet(self):
        return """
            QTableWidget
            {
                border: 1px solid #d3d7cf;
                border-radius: 0px;
                font-family: Noto Sans;
                font-size: 9pt;
                font-weight: bold;
                background-color: #eeeeec;
                color: #555753;
                selection-color: #ffffff
            }
            QTableWidget::item:hover
            {   
                color: #2e3436;
                background: qlineargradient(x1:0, y1:0, x2:1, y2:1, stop:0 #cfbb72, stop:1 #d3d7cf);           
            }
            
            QTableWidget::item:selected 
            {
                color: #ffffff;
                background: qlineargradient(x1:0, y1:0, x1:2, y1:2, stop:0 #204a87, stop:1 #729fcf);
            } 
            QStatusBar
            {
            height: 20px;
            font-size: 8pt;
            font-weight: bold;
            color: #324864;
            }
        """    
    
    if __name__ == '__main__':
        import sys
        app = QApplication(sys.argv)
        window = Window()
        window.show()
        if window.check_ffmpeg("ffmpeg") == False:
            QMessageBox.warning(window, "Error", "<b>ffmpeg not found</b><br><br><i>Please install ffmpeg</i>")
            window.handleQuit()
        else:
            window.statusBar().showMessage("Welcome to AudioConverterLinux *** found ffmpeg", 0)
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
