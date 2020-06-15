---
title: LED
date: 2020-05-07
---
Example Python program LED.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import QUrl, QTime, QTimer
* from PyQt5.QtGui import QIcon, QPixmap
* from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
* from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QVBoxLayout, QLCDNumber
* import sys

## Classes

* class DigitalClock(QLCDNumber):

## Methods

* def __init__(self, parent=None):
* def set_window_icon_from_response(self, http_response):
* def showTime(self):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5.QtCore import QUrl, QTime, QTimer
    from PyQt5.QtGui import QIcon, QPixmap
    from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
    from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QVBoxLayout, QLCDNumber
    
    ICON_IMAGE_URL = "https://www.google.ge/images/branding/product/ico/googleg_lodp.ico"
    class DigitalClock(QLCDNumber):
        def __init__(self, parent=None):
            super(DigitalClock, self).__init__(parent)
    
            self.setSegmentStyle(QLCDNumber.Filled)
    
            timer = QTimer(self)
            timer.timeout.connect(self.showTime)
            timer.start(1000)
    
            self.showTime()
    
            self.setWindowTitle("Aktuelle Stunde")
            self.resize(100, 100)
            QWidget.__init__(self)
    
            self.label = QLabel('')
    
            self.vertical_layout = QVBoxLayout()
            self.vertical_layout.addWidget(self.label)
    
            self.setLayout(self.vertical_layout)
    
            self.nam = QNetworkAccessManager()
            self.nam.finished.connect(self.set_window_icon_from_response)
            self.nam.get(QNetworkRequest(QUrl(ICON_IMAGE_URL)))
    
        def set_window_icon_from_response(self, http_response):
            pixmap = QPixmap()
            pixmap.loadFromData(http_response.readAll())
            icon = QIcon(pixmap)
            self.setWindowIcon(icon)
    
    
        def showTime(self):
            time = QTime.currentTime()
            text = time.toString('hh:mm')
            if (time.second() % 2) == 0:
                text = text[:2] + ' ' + text[3:]
    
            self.display(text)
    
    
    if __name__ == '__main__':
    
        import sys
    
        app = QApplication(sys.argv)
        clock = DigitalClock()
        clock.show()
    sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
