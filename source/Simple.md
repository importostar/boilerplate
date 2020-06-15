---
title: Simple
date: 2020-05-07
---
Example Python program Simple.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import QApplication , QLCDNumber
* from PyQt5.QtCore import QTimer , QTime
* from PyQt5.QtGui import QIcon , QColor
* import sys

## Classes

* class clock(QLCDNumber):

## Methods

* def __init__(self):
* def showTime(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QApplication , QLCDNumber
    from PyQt5.QtCore import QTimer , QTime
    from PyQt5.QtGui import QIcon , QColor
    import sys
    
    
    class clock(QLCDNumber):
        def __init__(self):
            super().__init__()
            title = 'Κύριλλος Clock'
            top = 400
            left = 400
            width = 450
            height = 300
    
            icon = 'clock.png'
            self.setWindowTitle(title)
            self.setGeometry(top, left , width , height)
            self.setWindowIcon(QIcon(icon))
    
            palete = self.palette()
            palete.setColor(palete.WindowText, QColor(204,204,0))
            palete.setColor(palete.Background ,QColor(0,0,255) )
            self.setPalette(palete)
            self.setSegmentStyle(QLCDNumber.Filled)
            timer = QTimer(self)
            timer.timeout.connect(self.showTime)
            timer.start(1000)
            self.showTime()
    
    
    
        def showTime(self):
             time = QTime.currentTime()
             text = time.toString('hh:mm')
             if (time.second() % 2 ) == 0 :
                 text = text[:2] + ' ' + text[3:]
             self.display(text)
    
    
    
    app = QApplication(sys.argv)
    clock = clock()
    clock.show()
    app.exec()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
