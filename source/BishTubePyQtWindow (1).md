---
title: BishTubePyQtWindow (1)
date: 2020-05-07
---
Example Python program BishTubePyQtWindow (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pyperclip
* import pytube
* from pytube.helpers import safe_filename
* import re
* import PyQt5
* from PyQt5 import QtWidgets
* from PyQt5 import QtCore
* from PyQt5 import QtGui
* import threading
* import os
* import sys
* import time
* import ffmpy
* import subprocess
* import os

## Classes

* class YT(QtWidgets.QDialog):
* class check_clip(threading.Thread):

## Methods

* def __init__ (self):
* def __init__ (self, window):
* def button_fun(self):
* def check_clipboard(self):
* def download(self):
* def convert_mp4_to_mp3(self):
* def run(self):

## Code

Example Python PyQt program :

    import pyperclip
    import pytube
    from pytube.helpers import safe_filename
    import re
    import PyQt5
    from PyQt5 import QtWidgets
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    import threading
    import os
    import sys
    import time
    import ffmpy
    import subprocess
    import os
    
    class YT(QtWidgets.QDialog):
        def __init__ (self):
            super().__init__()
            self.setFixedSize(600,150)
            self.setWindowTitle('BishTjub')
            self.setWindowFlags(QtCore.Qt.WindowStaysOnTopHint)
            self.setWindowIcon(QtGui.QIcon('icon.png'))
    
            self.song_title = QtWidgets.QLineEdit(self)
            self.song_title.setAlignment(QtCore.Qt.AlignCenter)
            self.song_title.resize(600,52)
            self.song_title.move(0,0)
            self.song_title.setReadOnly(1)
    
            self.song_path = QtWidgets.QLineEdit(self)
            self.song_path.setAlignment(QtCore.Qt.AlignCenter)
            self.song_path.resize(600,52)
            self.song_path.move(0,50)
           # with open('config.yt', 'r') as f:
              #  self.song_path.setText(str(f.readline()))
            self.song_path.setText("e:\\Muza\\new\\")
            
            self.button = QtWidgets.QPushButton("Download", self)
            self.button.resize(602, 52)
            self.button.move(0, 100)
    
    class check_clip(threading.Thread):
        def __init__ (self, window):
            super().__init__()
            self.w = window
            self.w.button.clicked.connect(self.button_fun)
            self.temp_addr = pyperclip.paste()
            self.yt_stream = None
            self.yt = None
            self.start_download = False
            self.convert = False
    
        def button_fun(self):
            if self.w.song_title.text() != '' and os.path.isdir(self.w.song_path.text()) == True:
                print('Downloading...')
                self.start_download = True
            else:
                print('Path or link error!')
    
        def check_clipboard(self):
            time.sleep(0.02)
            if self.temp_addr != pyperclip.paste() and re.match('^.*youtube.*', pyperclip.paste()):
                self.temp_addr = pyperclip.paste()
                self.yt = pytube.YouTube(self.temp_addr)
                self.yt_stream = self.yt.streams.filter(file_extension='mp4').first()
                self.w.song_title.setText(str(self.yt.title))
            else:
                pass
    
        def download(self):
            if self.start_download == True:
                    #self.w.song_title.setText('Downloading...')
                    self.yt_stream.download(self.w.song_path.text())
                    self.start_download = False
                    self.convert = True
            else:
                pass
    
        def convert_mp4_to_mp3(self):
            if self.convert == True:
    
                self.convert = False
                print('Converting to mp3...')
    
                source = self.w.song_path.text() + '\\' + safe_filename(self.yt.title) + '.mp4'
                dest = self.w.song_path.text() + '\\' + safe_filename(self.w.song_title.text()) + '.mp3'
                #self.w.song_title.setText('Converting to mp3...')
                try:
                    ff = ffmpy.FFmpeg(inputs = {source: None}, outputs={dest: '-y'})
                    ff.run()
                    os.remove(source)
                    w.song_title.setText('Done!')
                except:
                    self.w.song_title.setText('Download error!')
    
        def run(self):
            while 1:
                self.check_clipboard()
                self.download()
                self.convert_mp4_to_mp3()
    
    app = QtWidgets.QApplication([])
    w = YT()
    cc = check_clip(w)
    
    cc.daemon = True
    cc.start()
    w.show()
    w.exec()
    with open('config.yt', 'w') as a:
        a.write(str(w.song_path.text()))
    sys.exit()
    
    
            
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
