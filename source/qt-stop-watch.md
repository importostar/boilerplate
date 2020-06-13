---
title: qt stop watch
date: 2020-05-07
---
Example Python program qt-stop-watch.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* import getopt
* from PyQt5 import Qt
* from PyQt5.QtWidgets import QSystemTrayIcon, QStyle, QAction, QMenu, qApp
* from PyQt5.uic import loadUi
* from PyQt5.QtGui import QPixmap, QPainter, QFont, QIcon, QColor
* from PyQt5.QtCore import QPoint, QSize, QRectF
* from PyQt5.QtCore import Qt as CoreQt

## Classes

* class StopWatch(Qt.QMainWindow):

## Methods

* def __init__(self, parent=None):
* def keyPressEvent(self, event):
* def display(self):
* def iconActivated(self, reason):
* def drawOnIcon(self, text):
* def adaptFontSize(self, painter, flags, drawRect, text):
* def tick(self):
* def do_start(self):
* def do_pause(self):
* def do_reset(self):
* def usage():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    
    import sys
    import os
    import getopt
    
    from PyQt5 import Qt
    from PyQt5.QtWidgets import QSystemTrayIcon, QStyle, QAction, QMenu, qApp
    from PyQt5.uic import loadUi
    from PyQt5.QtGui import QPixmap, QPainter, QFont, QIcon, QColor
    from PyQt5.QtCore import QPoint, QSize, QRectF
    from PyQt5.QtCore import Qt as CoreQt
    
    # [ms]
    TICK_TIME = 2**6
    
    
    class StopWatch(Qt.QMainWindow):
        def __init__(self, parent=None):
            super().__init__(parent)
            self.ui = loadUi("gui.ui", self)
            self.reset.clicked.connect(self.do_reset)
            self.start.clicked.connect(self.do_start)
    
            self.timer = Qt.QTimer()
            self.timer.setInterval(TICK_TIME)
            self.timer.timeout.connect(self.tick)
    
            self.tray_icon = Qt.QSystemTrayIcon(self)
            self.tray_icon.setIcon(
                self.style().standardIcon(QStyle.SP_ComputerIcon))
            self.tray_icon.activated.connect(self.iconActivated)
    
            '''
                Define and add steps to work with the system tray icon
                show - show window
                hide - hide window
                exit - exit from application
            '''
            show_action = QAction("Show", self)
            quit_action = QAction("Exit", self)
            hide_action = QAction("Hide", self)
            show_action.triggered.connect(self.show)
            hide_action.triggered.connect(self.hide)
            quit_action.triggered.connect(qApp.quit)
    
            tray_menu = QMenu()
            tray_menu.addAction(show_action)
            tray_menu.addAction(hide_action)
            tray_menu.addAction(quit_action)
            self.tray_icon.setContextMenu(tray_menu)
            self.tray_icon.show()
    
            self.setGeometry(
                QStyle.alignedRect(
                    CoreQt.LeftToRight,
                    CoreQt.AlignCenter,
                    self.size(),
                    qApp.desktop().availableGeometry()
                )
            )
    
            self.do_reset()
    
        def keyPressEvent(self, event):
            if event.key() == Qt.Qt.Key_Escape:
                self.close()
            else:
                super().keyPressEvent(event)
    
        def display(self):
            seconds_frac = self.time % 60
            seconds = int(self.time % 60)
            minutes = int((self.time / 60) % 60)
            hours = int((self.time / (60 * 60)) % 24)
            self.lcd.display("{:d}:{:d}:{:05.2f}".format(hours, minutes, seconds_frac))
            self.drawOnIcon("{:d}:{:02d}".format(hours, minutes))
    
        def iconActivated(self, reason):
            if reason == QSystemTrayIcon.Trigger:
                self.show()
    
        def drawOnIcon(self, text):
            pixmap = QPixmap(QSize(100, 100))
            pixmap.fill(QColor(0, 0, 0, 0))
            painter = QPainter(pixmap)
            painter.setPen(QColor(255, 255, 255, 255))
            font = QFont("Monospace")
            font.setStyleHint(QFont.TypeWriter)
            painter.setFont(font)
            drawRect = QRectF(0, 0, 100, 100)
            self.adaptFontSize(painter, 0, drawRect, text)
            painter.drawText(drawRect, CoreQt.AlignCenter, text)
            painter.end()
            icon = QIcon(pixmap)
            self.tray_icon.setIcon(icon)
    
        def adaptFontSize(self, painter, flags, drawRect, text):
            flags = CoreQt.TextDontClip | CoreQt.TextWordWrap
            fontBoundRect = painter.fontMetrics().boundingRect(
                drawRect.toRect(), flags, text)
            xFactor = drawRect.width() / fontBoundRect.width()
            yFactor = drawRect.height() / fontBoundRect.height()
            factor = xFactor if xFactor < yFactor else yFactor
            f = painter.font()
            f.setPointSizeF(f.pointSizeF() * factor)
            painter.setFont(f)
    
        @Qt.pyqtSlot()
        def tick(self):
            self.time += TICK_TIME/1000
            self.display()
    
        @Qt.pyqtSlot()
        def do_start(self):
            self.timer.start()
            self.start.setText("Pause")
            self.start.clicked.disconnect()
            self.start.clicked.connect(self.do_pause)
    
        @Qt.pyqtSlot()
        def do_pause(self):
            self.timer.stop()
            self.start.setText("Start")
            self.start.clicked.disconnect()
            self.start.clicked.connect(self.do_start)
    
        @Qt.pyqtSlot()
        def do_reset(self):
            self.time = 0
            self.display()
    
    
    def usage():
        print("Usage: {} [OPTION]".format(os.path.split(sys.argv[0])[1]))
        print("    --start         auto start stopwatch")
        print("    --hidden        start hidden")
        print("    --help          display help")
    
    autostart = None
    hidden = None
    
    try:
        lOpts, lArgs = getopt.getopt(sys.argv[1:], "", ["help", "start", "hidden"])
    
        if len(lArgs) == 0:
            lArgs = [os.getcwd()]
    
        if ("--help", "") in lOpts:
            usage()
            sys.exit(None)
    
        if ("--start", "") in lOpts:
            autostart = True
    
        if ("--hidden", "") in lOpts:
            hidden = True
    
    except getopt.GetoptError as err:
        print(err)
        print()
        usage()
        sys.exit(2)
    
    app = Qt.QApplication(sys.argv)
    
    watch = StopWatch()
    watch.show()
    
    if autostart:
        watch.do_start()
    
    if hidden:
        watch.hide()
    
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
