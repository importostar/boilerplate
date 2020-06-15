---
title: pyTest (1)
date: 2020-05-07
---
Example Python program pyTest (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import ctypes
* from PyQt5.QtWidgets import QApplication, QWidget
* from PyQt5.QtGui import QFontDatabase, QFont, QFontMetrics, QImage, QPainter, QPen
* from PyQt5.QtCore import Qt, QRectF

## Code

Example Python PyQt program :

    import sys
    import ctypes
    from PyQt5.QtWidgets import QApplication, QWidget
    from PyQt5.QtGui import QFontDatabase, QFont, QFontMetrics, QImage, QPainter, QPen
    from PyQt5.QtCore import Qt, QRectF
    
    if __name__ == '__main__':
        
        app = QApplication(sys.argv)
    
        w = QWidget()
        w.resize(250, 150)
        w.move(300, 300)
        w.setWindowTitle('Simple')
        print(int(w.winId()))
    
        testDll = ctypes.CDLL('./testDll.dll')
        Test_Add_int = testDll.Test_Add_int
        Test_Add_int.argtypes = [ctypes.c_int, ctypes.c_int]
        Test_Add_int.restype = ctypes.c_int
        ret = Test_Add_int(2, 3)
    
        Test_Add_float = testDll.Test_Add_float
        Test_Add_float.argtypes = [ctypes.c_float, ctypes.c_float]
        Test_Add_float.restype = ctypes.c_float
        ret = Test_Add_float(2.1, 3.3)
    
        HWND_Func = testDll.HWND_Func
        HWND_Func.argtypes = [ctypes.c_uint32]
        HWND_Func(int(w.winId()))
    
        fonts = QFontDatabase().families()
        #for f in fonts:
        #    print(f)
    
        msg = "abcdefghijklmnopqrstuvwxyz"
        font = QFont("Tahoma")
        font.setUnderline(False)
        font.setPointSize(20)
        image = QImage(500, 100, QImage.Format_ARGB32_Premultiplied)
        painter = QPainter(image)
        painter.setFont(font)
        painter.fillRect(image.rect(), Qt.white)
        x = image.rect().x()
        y = image.rect().y()
        painter.drawText(image.rect(), Qt.AlignLeft | Qt.AlignTop, msg)
        metric = QFontMetrics(font)
        pen = QPen(Qt.red)
        painter.setPen(pen)
        for c in msg:
            r = QRectF(x, y, metric.width(c), metric.height())
            painter.drawRect(r)
            x += metric.width(c)
        image.save("output.png")
    
        w.show()
        
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
