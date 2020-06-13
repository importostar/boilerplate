---
title: Countdown
date: 2020-05-07
---
Example Python program Countdown.py
This program creates a PyQt GUI

## Modules

* import ctypes
* import os
* import platform
* from datetime import datetime
* import sys
* from PyQt5.QtCore import QTimer
* from PyQt5.QtWidgets import *

## Classes

* class Utils:
* class MainWindow(QMainWindow):
* class MainWidget(QWidget):

## Methods

* def showMessageBox(self, title, message):
* def showHintBox(self, message):
* def __init__(self):
* def initUI(self):
* def center(self):
* def closeEvent(self, event):
* def __init__(self):
* def initUI(self):
* def start(self):
* def start_timer(self):
* def lockWorkStation(self):
* def halt(self):
* def stop(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    import ctypes
    import os
    import platform
    from datetime import datetime
    
    import sys
    from PyQt5.QtCore import QTimer
    from PyQt5.QtWidgets import *
    
    
    class Utils:
        @staticmethod
        def showMessageBox(self, title, message):
            return QMessageBox.question(self, title,
                                        message, QMessageBox.Yes |
                                        QMessageBox.No, QMessageBox.No)
    
        @staticmethod
        def showHintBox(self, message):
            return QMessageBox.question(self, "提示",
                                        message, QMessageBox.Yes, QMessageBox.Yes)
    
    
    class MainWindow(QMainWindow):
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            self.setCentralWidget(MainWidget())
    
            exitAction = QAction('&Exit', self)
            exitAction.setShortcut('Ctrl+Q')
            exitAction.setStatusTip('Exit application')
            exitAction.triggered.connect(self.close)
    
            menubar = self.menuBar()
            fileMenu = menubar.addMenu('&Info')
            fileMenu.addAction(exitAction)
    
            self.setGeometry(300, 300, 300, 200)
            # self.setWindowIcon(QIcon('Application-icon.png'))
            self.setWindowTitle('Main')
            self.center()
            self.show()
    
        def center(self):
            qr = self.frameGeometry()
            cp = QDesktopWidget().availableGeometry().center()
            qr.moveCenter(cp)
            self.move(qr.topLeft())
    
        def closeEvent(self, event):
            reply = Utils.showMessageBox(self, 'Message', "是否退出?")
    
            if reply == QMessageBox.Yes:
                event.accept()
            else:
                event.ignore()
    
    
    class MainWidget(QWidget):
        msg = "<span style='font-size: 15px'>多少秒后开始 : </span> <span style='font-size: 30px;'>  {:d} </span>"
        is_start = False
    
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            self.text = QLabel()
    
            operation_label = QLabel("执行操作：")
            self.operationComboBox = QComboBox()
            self.operationComboBox.insertItem(0, self.tr("关机"))
            self.operationComboBox.insertItem(1, self.tr("锁定"))
            operation_layout = QHBoxLayout()
            operation_layout.addWidget(operation_label)
            operation_layout.addWidget(self.operationComboBox)
    
            self.start_btn = QPushButton("开始")
            self.start_btn.clicked.connect(self.start)
            now = datetime.now()
    
            start_time_label = QLabel("开始时间：")
    
            self.month_edit = QTextEdit()
            self.month_edit.setFixedHeight(25)
            self.month_edit.setFixedWidth(25)
            month_label = QLabel("月")
            self.month_edit.setText(str(now.month))
    
            self.day_edit = QTextEdit()
            self.day_edit.setFixedHeight(25)
            self.day_edit.setFixedWidth(25)
            day_label = QLabel("日")
            self.day_edit.setText(str(now.day))
    
            self.hour_edit = QTextEdit()
            self.hour_edit.setFixedHeight(25)
            self.hour_edit.setFixedWidth(25)
            hour_label = QLabel("小时")
            self.hour_edit.setText(str(now.hour))
    
            self.minute_edit = QTextEdit()
            self.minute_edit.setFixedHeight(25)
            self.minute_edit.setFixedWidth(25)
            minute_label = QLabel("分钟")
            self.minute_edit.setText(str(now.minute))
    
            layout = QHBoxLayout()
            layout.addWidget(self.month_edit)
            layout.addWidget(month_label)
            layout.addWidget(self.day_edit)
            layout.addWidget(day_label)
            layout.addWidget(self.hour_edit)
            layout.addWidget(hour_label)
            layout.addWidget(self.minute_edit)
            layout.addWidget(minute_label)
            layout.addWidget(self.start_btn)
    
            hbox = QVBoxLayout()
            hbox.addLayout(operation_layout)
            hbox.addWidget(start_time_label)
            hbox.addLayout(layout)
            hbox.addWidget(self.text)
    
            self.text.setText(self.msg.format(0))
    
            self.setLayout(hbox)
    
        def start(self):
            if (self.is_start):
                self.stop()
            else:
                month = self.month_edit.toPlainText()
                day = self.day_edit.toPlainText()
                hour = self.hour_edit.toPlainText()
                minute = self.minute_edit.toPlainText()
                self.start_datetime = datetime(datetime.now().year, int(month), int(day), int(hour), int(minute))
                now_datetime = datetime.now()
                if (self.start_datetime.time() > now_datetime.time()):
                    seconds = (self.start_datetime - now_datetime).total_seconds()
                    self.text.setText(self.msg.format(int(seconds)))
                    self.is_start = True
                    self.start_btn.setText("取消")
                    self.timer = QTimer(self)
                    self.timer.timeout.connect(self.start_timer)
                    self.timer.start(1000)  # 1000 miliseconds = 1 second
                else:
                    Utils.showHintBox(self, "开始时间小于当前时间")
    
        def start_timer(self):
            now_datetime = datetime.now()
            if (self.start_datetime.time() > now_datetime.time()):
                seconds = (self.start_datetime - now_datetime).total_seconds()
                self.text.setText(self.msg.format(int(seconds)))
            else:
                if (self.operationComboBox.currentIndex() == 0):
                    self.halt()
                    sys.exit()
                elif (self.operationComboBox.currentIndex() == 1):
                    self.stop()
                    self.lockWorkStation()
    
        def lockWorkStation(self):
            sysstr =platform.system()
            if (sysstr == "Windows"):
                user32 = ctypes.windll.LoadLibrary('user32.dll')
                user32.LockWorkStation()
            elif (sysstr == "Linux"):
                pass
    
        def halt(self):
            sysstr = platform.system()
            if (sysstr == "Windows"):
                os.system("cmd.exe /k shutdown -s -t 0")
            elif (sysstr == "Linux"):
                # os.system('halt')
                pass
    
        def stop(self):
            if (self.timer.isActive()):
                self.timer.stop()
            self.is_start = False
            self.text.setText(self.msg.format(0))
            self.start_btn.setText("开始")
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        main = MainWindow()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
