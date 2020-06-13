---
title: pyqtani
date: 2020-05-07
---
Example Python program pyqtani.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import io
* import time
* import threading
* import cv2
* from PyQt5.QtCore import Qt
* from PyQt5.QtWidgets import (
* from PyQt5.QtGui import (
* from PyQt5.QtCore import (
* from PIL import Image

## Classes

* class Example(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def runRendering(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    
    import sys
    import io
    import time
    import threading
    import cv2
    
    from PyQt5.QtCore import Qt
    from PyQt5.QtWidgets import (
        QWidget,
        QLabel,
        QVBoxLayout,
        QApplication
    )
    from PyQt5.QtGui import (
        QPixmap
    )
    from PyQt5.QtCore import (
        QByteArray
    )
    
    from PIL import Image
    
    class Example(QWidget):
        
        def __init__(self):
            super().__init__()
            self.pixmap = QPixmap()
            self.label = QLabel(self)
            self.initUI()
            threading.Thread(target = self.runRendering).start()
            
        def initUI(self):
            vbox = QVBoxLayout()
            vbox.addWidget(self.label)
            self.setLayout(vbox)
            self.setGeometry(300, 300, 250, 150)
            self.setWindowTitle('PyQt5 Window')
            self.show()
    
        def runRendering(self):
            """ 异步渲染的线程
            """
            # 如果要从摄像头读取数据，就是 self.cam = cv2.VideoCapture(0)
            self.cam = cv2.VideoCapture('./badapple.mp4')
            while True: # 渲染循环:
                ret, frm = self.cam.read()
                if not ret:
                    print('Video ends')
                    break
                im = Image.fromarray(frm)
                buf = io.BytesIO()
                im.save(buf, 'BMP')
                buf.flush()
                self.pixmap.loadFromData(QByteArray(buf.getvalue()))
                self.label.setPixmap(self.pixmap)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = Example()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
