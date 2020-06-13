---
title: stackoverflow_question
date: 2020-05-07
---
Example Python program stackoverflow_question.py
This program creates a PyQt GUI

## Modules

* import sys
* import urllib.request
* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *

## Classes

* class Downloader(QDialog):

## Methods

* def __init__(self):
* def download(self):
* def report(self, blocknum, blocksize, totalsize):

## Code

Example Python PyQt program :

    import sys
    import urllib.request
    
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    
    
    class Downloader(QDialog):
        def __init__(self):
            QDialog.__init__(self)
            layout = QVBoxLayout()
            self.url = QLineEdit()
            self.save_location = QLineEdit()
            self.progress = QProgressBar()
            download = QPushButton("Download")
            self.progress.setValue(0)
            self.progress.setAlignment(Qt.AlignHCenter)
    
            self.url.setPlaceholderText("URL")
            self.save_location.setPlaceholderText("Save folder:")
    
            layout.addWidget(self.url)
            layout.addWidget(self.save_location)
            layout.addWidget(self.progress)
            layout.addWidget(download)
            self.setLayout(layout)
            self.setWindowTitle("Downloader")
            download.clicked.connect(self.download)
    
        def download(self):
            url = self.url.text()
            save_location = self.save_location.text()
            urllib.request.urlretrieve(url, save_location, self.report)
    
            try:
                urllib.request.urlretrieve(url, save_location, self.report)
            except Exception:
                QMessageBox.warning(self, "Warning", "The download failed")
                return
    
            QMessageBox.information(self, "Information", "Download is complete")
            self.progress.setValue(0)
            self.url.setText("")
            self.save_location.setText("")
    
        def report(self, blocknum, blocksize, totalsize):
            readsofar = blocknum * blocksize
            if totalsize > 0:
                percent = readsofar * 100 / totalsize
                self.progress.setValue(int(percent))
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        dl = Downloader()
        dl.show()
        app.exec_()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
