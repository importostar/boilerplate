---
title: nsd
date: 2020-05-07
---
Example Python program nsd.py
This program creates a PyQt GUI

## Modules

* import multiprocessing
* import sys
* import threading
* import time
* from PyQt5 import QtCore
* from PyQt5 import QtGui
* from PyQt5 import QtWidgets
* import AppKit
* import random

## Classes

* class OutlinedLabel(QtWidgets.QLabel):
* class Comment(QtWidgets.QMainWindow):

## Methods

* def paintEvent(self, *args, **kwargs):
* def __init__(self, app, message):
* def start(self, y):
* def move_next(self):
* def _hideMacDockIcon():
* def _main(message):
* def _child_waiter():
* def main():

## Code

Example Python PyQt program :

    '''Niconico Style Display
    
    requirements:
        PyQt5
        pyobjc-framework-Cocoa (pyobjc-cocoa?, osx only)
    '''
    
    import multiprocessing
    import sys
    import threading
    import time
    
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    from PyQt5 import QtWidgets
    
    
    class OutlinedLabel(QtWidgets.QLabel):
        def paintEvent(self, *args, **kwargs):
            # TODO: text containing newline characters
            painter = QtGui.QPainter(self)
            path = QtGui.QPainterPath()
            pen = QtGui.QPen()
            font = self.font()
    
            # XXX: really?
            y = (font.pixelSize() + self.height()) / 2
    
            pen.setWidth(1)
            pen.setColor(QtCore.Qt.black)
            painter.setFont(font)
            painter.setPen(pen)
            painter.setRenderHints(
                QtGui.QPainter.Antialiasing | QtGui.QPainter.TextAntialiasing)
    
            path.addText(0, y, font, self.text())
            painter.fillPath(path, QtCore.Qt.white)
            painter.drawPath(path)
    
    
    class Comment(QtWidgets.QMainWindow):
        font = 'Sans Serif'
        font_size = 24
        fps = 60
        duration = 10
    
        def __init__(self, app, message):
            super(Comment, self).__init__()
    
            self.setWindowFlags(self.windowFlags() |
                                QtCore.Qt.FramelessWindowHint |
                                QtCore.Qt.BypassWindowManagerHint |
                                QtCore.Qt.WindowStaysOnTopHint)
            self.setAttribute(QtCore.Qt.WA_TranslucentBackground)
            self.setFocusPolicy(QtCore.Qt.NoFocus)
    
            self.app = app
    
            self.label = OutlinedLabel()
            font = QtGui.QFont(self.font, self.font_size, QtGui.QFont.Bold)
            self.label.setFont(font)
            palette = QtGui.QPalette()
            palette.setColor(palette.Foreground, QtCore.Qt.white)
            self.label.setPalette(palette)
            self.label.setText(message)
    
            self.setCentralWidget(self.label)
    
        def start(self, y):
            desktop = QtWidgets.QDesktopWidget()
            resolution = desktop.screenGeometry()
            self.x = resolution.width()
            self.y = y
    
            self.move(self.x, self.y)
    
            self.show()
            self.label.show()
    
            self.step = (self.x + self.size().width()) / (self.duration * self.fps)
    
            self.timer = QtCore.QTimer()
            self.timer.timeout.connect(self.move_next)
            self.timer.start(16)
    
        def move_next(self):
            self.x -= self.step
            self.move(self.x, self.y)
    
            if self.x < -self.size().width():
                self.timer.stop()
                self.hide()
                self.destroy()
    
                self.app.exit()
    
    
    def _hideMacDockIcon():
        if sys.platform != 'darwin':
            return
    
        import AppKit
        info = AppKit.NSBundle.mainBundle().infoDictionary()
        info["LSBackgroundOnly"] = "1"
    
    
    def _main(message):
        import random
    
        _hideMacDockIcon()
    
        app = QtWidgets.QApplication(sys.argv)
    
        desktop = QtWidgets.QDesktopWidget()
        resolution = desktop.screenGeometry()
    
        comment = Comment(app, message)
        comment.start(random.randint(100, resolution.height()-200))
    
        sys.exit(app.exec_())
    
    
    def _child_waiter():
        # wait for chailds (needs on osx only?)
        while True:
            multiprocessing.active_children()
            time.sleep(3)
    
    
    def main():
        MAX_NUM_COMMENTS = 50
    
        threading.Thread(target=_child_waiter, daemon=True).start()
    
        for i, line in enumerate(sys.stdin, 1):
            line = line.rstrip('\r\n')
            # XXX: because moving many windows on same process is too slow on PyQt,
            #      spawn process for each windows.
            p = multiprocessing.Process(name=i, target=_main, args=(line, ))
            p.start()
    
            active_comments = multiprocessing.active_children()
    
            if len(active_comments) > MAX_NUM_COMMENTS:
                active_comments.sort(key=lambda c: c.name)
                active_comments[0].terminate()
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
