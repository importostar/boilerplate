---
title: pyrei
date: 2020-05-07
---
Example Python program pyrei.py
This program creates a PyQt GUI

## Modules

* from __future__ import division
* from PyQt5.QtWidgets import QApplication, QWidget, QGridLayout, QLabel
* from PyQt5.QtCore import QTimer, Qt
* import time, sys

## Methods

* def getime():
* def day_week():
* def data_list():
* def atTimeOut():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    #coding = utf-8
    from __future__ import division
    from PyQt5.QtWidgets import QApplication, QWidget, QGridLayout, QLabel
    from PyQt5.QtCore import QTimer, Qt
    import time, sys
    
    def getime():
        return time.localtime(time.time())
    
    def day_week():
        a = getime()
        if a[3] < 12:
            b = 60 * int(a[4]) + 3600 * int(a[3]) + int(a[5])
        elif a[3] == 12 or (a[3] == 13 and 0 <= a[4] < 20):
            b = 43200
        else:
            b = 60 * int(a[4]) + 3600 * int(a[3]) + int(a[5]) - 4800
        X = '%.4f' %((b - 27600) / 28800)
        if a[6] < 6:
            c = a[6]
        Y = (c + float(X)) / 5
        return [X, Y]
    
    def data_list():
        X, Y = day_week()
        past_day = str(round((100 * float(X)), 2)) + '%'
        earn_day = str(round((200 * float(X)), 2)) + 'E'
        past_week = str(round((100 * float(Y)), 2)) + '%'
        earn_week = str(round((1000 * float(Y)), 2)) + 'E'
        return [past_day, earn_day, past_week, earn_week]
    
    def atTimeOut():
        data_list_os = data_list()
        grid_label_1.setText(data_list_os[0])
        grid_label_2.setText(data_list_os[1])
        grid_label_3.setText(data_list_os[2])
        grid_label_4.setText(data_list_os[3])
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        window = QWidget()
        window.resize(120, 60)
        window.move(1400, 750)
        window.setWindowFlags(window.windowFlags() | Qt.WindowStaysOnTopHint)
        window.setWindowFlags(window.windowFlags() | Qt.FramelessWindowHint)
        window.setWindowFlags(window.windowFlags() | Qt.MSWindowsFixedSizeDialogHint)
        window.setWindowTitle("Flyme")
        grid = QGridLayout()
        data_list_os = data_list()
        grid_label_1 = QLabel(data_list_os[0])
        grid_label_2 = QLabel(data_list_os[1])
        grid_label_3 = QLabel(data_list_os[2])
        grid_label_4 = QLabel(data_list_os[3])
        grid.addWidget(grid_label_1, 0, 0)
        grid.addWidget(grid_label_2, 0, 1)
        grid.addWidget(grid_label_3, 1, 0)
        grid.addWidget(grid_label_4, 1, 1)
        window.setLayout(grid)
        window.timer = QTimer()
        window.timer.setInterval(1000)
        window.timer.start()
        window.timer.timeout.connect(lambda: atTimeOut())
        window.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
