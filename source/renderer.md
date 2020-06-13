---
title: renderer
date: 2020-05-07
---
Example Python program renderer.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import cv2
* import numpy as np
* from PyQt5.QtCore import QUrl, Qt
* from PyQt5.QtGui import QImage, QPainter
* from PyQt5.QtWebEngineWidgets import QWebEngineSettings, QWebEngineView
* from PyQt5.QtWidgets import QApplication

## Classes

* class MyWebView(QWebEngineView):

## Methods

* def __init__(self, parent=None):
* def load(self, url, callback=None):
* def display(self, finished):

## Code

Example Python PyQt program :

    import sys
    
    import cv2
    import numpy as np
    from PyQt5.QtCore import QUrl, Qt
    from PyQt5.QtGui import QImage, QPainter
    from PyQt5.QtWebEngineWidgets import QWebEngineSettings, QWebEngineView
    from PyQt5.QtWidgets import QApplication
    
    
    class MyWebView(QWebEngineView):
        def __init__(self, parent=None):
            QWebEngineView.__init__(self, parent)
            self.setAttribute(Qt.WA_DontShowOnScreen, True)
            self.setAttribute(Qt.WA_DeleteOnClose, True)
            self.show()
    
            QWebEngineSettings.globalSettings().setAttribute(QWebEngineSettings.PluginsEnabled, True)
            QWebEngineSettings.globalSettings().setAttribute(QWebEngineSettings.ScreenCaptureEnabled, True)
    
        def load(self, url, callback=None):
            super().load(url)
            self.loadFinished.connect(self.display)
    
        def display(self, finished):
            if finished:
                size = self.contentsRect()
                img = QImage(size.width(), size.height(), QImage.Format_ARGB32)
                painter = QPainter(img)
                self.render(painter)
                painter.end()
    
                ptr = img.bits()
                ptr.setsize(img.byteCount())
                arr = np.asarray(ptr, dtype=np.ubyte).reshape(img.height(), img.width(), 4)
                cv2.imshow(f"Image {img.width()}x{img.height()}", arr)
                cv2.waitKey(0)
    
            else:
                print("Error")
            self.close()
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
    
        width, height = 320, 640
        webview = MyWebView()
        webview.setGeometry(5, 30, width, height)
        webview.load(QUrl("https://hostgator.com"))
        app.exec()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
