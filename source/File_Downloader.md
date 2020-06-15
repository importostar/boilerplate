---
title: File_Downloader
date: 2020-05-07
---
Example Python program File_Downloader.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* import sys
* import urllib.request

## Classes

* class Downloader(QDialog):

## Methods

* def __init__(self):
* def download(self):
* def report(self,blocknum, blocksize, totalsize):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    import sys
    import urllib.request
    
    # This sets up the project as a modified instance of the QDialog Class
    class Downloader(QDialog):
        def __init__(self):
            # again, the new class needs to inherit from QDialog, so that gets initialized here
            QDialog.__init__(self)
    
            # this is the "window" type designator
            layout = QVBoxLayout()
    
            #instance variable of a URL bar
            self.url = QLineEdit()
    
            #instance variable of the save location bar
            self.save_location = QLineEdit()
    
            # instance variable of the progress bar
            self.progress = QProgressBar()
            download_button = QPushButton("Download!!")
    
            self.url.setPlaceholderText("URL")
            self.save_location.setPlaceholderText("File save location")
    
            self.progress.setValue(0)
            self.progress.setAlignment(Qt.AlignCenter)
    
            layout.addWidget(self.url)
            layout.addWidget(self.save_location)
            layout.addWidget(self.progress)
            layout.addWidget(download_button)
    
            download_button.clicked.connect(self.download)
    
            self.setLayout(layout)
            self.setWindowTitle("Pydownloader Bitches")
            self.setFocus()
    
        def download(self):
            url = self.url.text()
            save_location = self.save_location.text()
            urllib.request.urlretrieve(url,save_location,self.report)
    
        def report(self,blocknum, blocksize, totalsize):
            readsofar = blocknum * blocksize
            if totalsize > 0:
                percent = readsofar * 100 / totalsize
                self.progress.setValue(int(percent))
    
    app = QApplication(sys.argv)
    dl = Downloader()
    dl.show()
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
