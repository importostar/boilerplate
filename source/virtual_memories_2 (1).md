---
title: virtual_memories_2 (1)
date: 2020-05-07
---
Example Python program virtual_memories_2 (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import time
* import io
* import traceback
* from PyQt5.QtWidgets import QMessageBox
* import os
* import sys

## Classes

* class Ui_hGUI(QtWidgets.QWidget):

## Methods

* def __init__(self):
* def setupUi(self, hGUI):
* def retranslateUi(self, hGUI):
* def widget_close(self):
* def widget_minimize(self):
* def qt_message_handler(mode, context, message):
* def excepthook(excType, excValue, tracebackobj):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'C:\Users\Master\Desktop\Virtual Memories\virtualmemories___.ui'
    #
    # Created by: PyQt5 UI code generator 5.7
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_hGUI(QtWidgets.QWidget):
        def __init__(self):
            QtWidgets.QWidget.__init__(self)
    
            self.widget_title = "Virtual Memories"
            self.widget_version = "1.0.0"
    
            self.image_button_close = "imgs/button_close.png"
            self.image_button_close_hover = "imgs/button_close_hover.png"
            self.image_button_minimize = "imgs/button_minimize.png"
            self.image_button_minimize_hover = "imgs/button_minimize_hover.png"
            self.image_button_screenshot = "imgs/button_screenshot.png"
            self.image_button_screenshot_hover = "imgs/button_screenshot_hover.png"
            self.image_button_imgur = "imgs/button_imgur.png"
            self.image_button_imgur_hover = "imgs/button_imgur_hover.png"
    
            self.tooltip_button_close = "Close"
            self.tooltip_button_minimize = "Minimise"
            self.tooltip_button_screenshot = "Capture screen area"
            self.tooltip_button_imgur = "Go to imgur.com"
            self.tooltip_label_link = "Double click to copy"
            self.tooltip_label_version = "Current version"
            
        def setupUi(self, hGUI):
            hGUI.setObjectName("hGUI")
            hGUI.resize(161, 172)
            hGUI.setMinimumSize(QtCore.QSize(161, 172))
            hGUI.setMaximumSize(QtCore.QSize(161, 172))
            hGUI.setStyleSheet("QWidget#hGUI {\n"
    "    background-color: #000;\n"
    "    color: #FFF;\n"
    "    border-radius: 5px;\n"
    "    font: 75 8pt \"Berlin Sans FB\";\n"
    "}\n"
    "\n"
    "QPushButton#btn_screenshot {\n"
    "    background-color: #000;\n"
    "}\n"
    "\n"
    "QPushButton#btn_imgur {\n"
    "    background-color: #000;\n"
    "}\n"
    "\n"
    "QPushButton#btn_close {\n"
    "    background-color: #000;\n"
    "    border: 1px solid #2E8B57;\n"
    "}\n"
    "\n"
    "QPushButton#btn_close::hover {\n"
    "    background-color: #000;\n"
    "    border: 1px solid #8FBC8F;\n"
    "}\n"
    "\n"
    "QPushButton#btn_minimize {\n"
    "    background-color: #000;\n"
    "    border: 1px solid #2E8B57;\n"
    "}\n"
    "\n"
    "QPushButton#btn_minimize::hover {\n"
    "    background-color: #000;\n"
    "    border: 1px solid #8FBC8F;\n"
    "}\n"
    "\n"
    "QPushButton#btn_frame {\n"
    "    background-color: #000;\n"
    "}\n"
    "\n"
    "QLabel#lbl_link_ {\n"
    "    color: #FFD700;\n"
    "    font-weight: bold;\n"
    "    font-style: italic;\n"
    "    font: 8pt \"Cooper Black\";\n"
    "}    \n"
    "\n"
    "QLabel#lbl_link {\n"
    "    color: #8FBC8F;\n"
    "    font: 9pt \"David\";\n"
    "}\n"
    "\n"
    "QLabel#lbl_link::hover {\n"
    "    color: #98FB98;\n"
    "}\n"
    "\n"
    "QLabel#lbl_version {\n"
    "    color: #98FB98; /*\' light green */\n"
    "    font: 7pt \"Nirmala UI\";\n"
    "    font-style: italic;\n"
    "}\n"
    "\n"
    "QLabel#lbl_copy {\n"
    "    color: #FFF;\n"
    "}\n"
    "\n"
    "QCheckBox {\n"
    "    color: #FFF;\n"
    "    font: 8pt \"Arial\";\n"
    "}")
            self.btn_close = QtWidgets.QPushButton(hGUI)
            self.btn_close.setGeometry(QtCore.QRect(141, 0, 20, 20))
            font = QtGui.QFont()
            font.setBold(True)
            font.setWeight(75)
            self.btn_close.setFont(font)
            self.btn_close.setText("")
            icon = QtGui.QIcon()
            icon.addPixmap(QtGui.QPixmap(self.image_button_close), QtGui.QIcon.Normal, QtGui.QIcon.Off)
            self.btn_close.setIcon(icon)
            self.btn_close.setIconSize(QtCore.QSize(10, 10))
            self.btn_close.setObjectName("btn_close")
            self.btn_minimize = QtWidgets.QPushButton(hGUI)
            self.btn_minimize.setGeometry(QtCore.QRect(121, 0, 20, 20))
            font = QtGui.QFont()
            font.setFamily("Rod")
            self.btn_minimize.setFont(font)
            self.btn_minimize.setText("")
            icon1 = QtGui.QIcon()
            icon1.addPixmap(QtGui.QPixmap(self.image_button_minimize), QtGui.QIcon.Normal, QtGui.QIcon.Off)
            self.btn_minimize.setIcon(icon1)
            self.btn_minimize.setIconSize(QtCore.QSize(10, 10))
            self.btn_minimize.setObjectName("btn_minimize")
            self.lbl_version = QtWidgets.QLabel(hGUI)
            self.lbl_version.setGeometry(QtCore.QRect(90, 0, 31, 16))
            font = QtGui.QFont()
            font.setFamily("Nirmala UI")
            font.setPointSize(7)
            font.setBold(False)
            font.setItalic(True)
            font.setWeight(50)
            self.lbl_version.setFont(font)
            self.lbl_version.setObjectName("lbl_version")
            self.lbl_link_ = QtWidgets.QLabel(hGUI)
            self.lbl_link_.setGeometry(QtCore.QRect(10, 140, 141, 16))
            self.lbl_link_.setObjectName("lbl_link_")
            self.lbl_link = QtWidgets.QLabel(hGUI)
            self.lbl_link.setGeometry(QtCore.QRect(10, 150, 151, 20))
            self.lbl_link.setObjectName("lbl_link")
            self.btn_screenshot = QtWidgets.QPushButton(hGUI)
            self.btn_screenshot.setGeometry(QtCore.QRect(30, 40, 101, 81))
            self.btn_screenshot.setText("")
            icon2 = QtGui.QIcon()
            icon2.addPixmap(QtGui.QPixmap(self.image_button_screenshot), QtGui.QIcon.Normal, QtGui.QIcon.Off)
            self.btn_screenshot.setIcon(icon2)
            self.btn_screenshot.setIconSize(QtCore.QSize(100, 100))
            self.btn_screenshot.setObjectName("btn_screenshot")
            self.btn_imgur = QtWidgets.QPushButton(hGUI)
            self.btn_imgur.setGeometry(QtCore.QRect(4, 4, 61, 21))
            self.btn_imgur.setText("")
            icon3 = QtGui.QIcon()
            icon3.addPixmap(QtGui.QPixmap(self.image_button_imgur), QtGui.QIcon.Normal, QtGui.QIcon.Off)
            self.btn_imgur.setIcon(icon3)
            self.btn_imgur.setIconSize(QtCore.QSize(50, 50))
            self.btn_imgur.setObjectName("btn_imgur")
    
            self.retranslateUi(hGUI)
            QtCore.QMetaObject.connectSlotsByName(hGUI)
    
        def retranslateUi(self, hGUI):
            _translate = QtCore.QCoreApplication.translate
            hGUI.setWindowTitle(_translate("hGUI", "Virtual Memories"))
            self.btn_close.setToolTip(_translate("hGUI", self.tooltip_button_close))
            self.btn_minimize.setToolTip(_translate("hGUI", self.tooltip_button_minimize))
            self.lbl_version.setToolTip(_translate("hGUI", self.tooltip_label_version))
            self.lbl_version.setText(_translate("hGUI", "V1.0.0"))
            self.lbl_link_.setText(_translate("hGUI", "LINK - NOT COPIED"))
            self.lbl_link.setToolTip(_translate("hGUI", self.tooltip_label_link))
            self.lbl_link.setText(_translate("hGUI", "Screenshot not taken"))
            self.btn_screenshot.setToolTip(_translate("hGUI", self.tooltip_button_screenshot))
            self.btn_imgur.setToolTip(_translate("hGUI", self.tooltip_button_imgur))
    
            self.btn_close.clicked.connect(self.widget_close)
            self.btn_minimize.clicked.connect(self.widget_minimize)
    
        def widget_close(self):
            sys.exit(app.exec_())
    
        def widget_minimize(self):
            if self.windowState() != Qt.WindowMinimized:
                self.setWindowState(Qt.WindowMinimized)
                self.showMinimized()
            else:
                self.setWindowState(Qt.WindowNoState)
    
    # http://stackoverflow.com/a/35902894/228539
    def qt_message_handler(mode, context, message):
        if mode == QtCore.QtInfoMsg:
            mode = 'INFO'
        elif mode == QtCore.QtWarningMsg:
            mode = 'WARNING'
        elif mode == QtCore.QtCriticalMsg:
            mode = 'CRITICAL'
        elif mode == QtCore.QtFatalMsg:
            mode = 'FATAL'
        else:
            mode = 'DEBUG'
        print('qt_message_handler: line: %d, func: %s(), file: %s' % (
              context.line, context.function, context.file))
        print('  %s: %s\n' % (mode, message))
    
    QtCore.qInstallMessageHandler(qt_message_handler)
    import time
    import io
    import traceback
    from PyQt5.QtWidgets import QMessageBox
    import os
    # TODO: Consider updating from...
    #       http://die-offenbachs.homelinux.org:48888/hg/eric/file/a1e53a9ffcf3/eric6.py#l134
    
    # TODO: deal with licensing for swiped code (GPL3)
    #       http://die-offenbachs.homelinux.org:48888/hg/eric/file/a1e53a9ffcf3/LICENSE.GPL3
    
    def excepthook(excType, excValue, tracebackobj):
        """
        Global function to catch unhandled exceptions.
        @param excType exception type
        @param excValue exception value
        @param tracebackobj traceback object
        """
        separator = '-' * 70
        email = "kyle.altendorf@epcpower.com"
    
        try:
            hash = 'Revision Hash: {}\n\n'.format(epyq.revision.hash)
        except:
            hash = ''
    
        notice = \
            """An unhandled exception occurred. Please report the problem via email to:\n"""\
            """\t\t{email}\n\n{hash}"""\
            """A log has been written to "".\n\nError information:\n""".format(
            email=email, hash=hash)#, log=log.name)
        # TODO: add something for version
        versionInfo=""
        timeString = time.strftime("%Y-%m-%d, %H:%M:%S")
    
        tbinfofile = io.StringIO()
        traceback.print_tb(tracebackobj, None, tbinfofile)
        tbinfofile.seek(0)
        tbinfo = tbinfofile.read()
        errmsg = '%s: \n%s' % (str(excType), str(excValue))
        sections = [separator, timeString, separator, errmsg, separator, tbinfo]
        msg = '\n'.join(sections)
    
        errorbox = QMessageBox()
        errorbox.setWindowTitle("EPyQ")
        errorbox.setIcon(QMessageBox.Critical)
    
        # TODO: CAMPid 980567566238416124867857834291346779
        # ico_file = os.path.join(QFileInfo.absolutePath(QFileInfo(__file__)), 'icon.ico')
        # ico = QtGui.QIcon(ico_file)
        # errorbox.setWindowIcon(ico)
    
        complete = str(notice) + str(msg) + str(versionInfo)
    
        sys.stderr.write(complete)
        errorbox.setText(complete)
        errorbox.exec_()
    
    
    if __name__ == "__main__":
        import sys
    
        sys.excepthook = excepthook
    
        app = QtWidgets.QApplication(sys.argv)
        hGUI = QtWidgets.QWidget(flags = QtCore.Qt.FramelessWindowHint)
        ui = Ui_hGUI()
        ui.setupUi(hGUI)
        hGUI.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
