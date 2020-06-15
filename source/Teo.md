---
title: Teo
date: 2020-05-07
---
Example Python program Teo.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import (QApplication, QWidget,
* from PyQt5.QtCore import QCoreApplication
* from PyQt5.QtGui import QIcon
* from PyQt5.QtGui import QFont

## Classes

* class Example(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def center(self):
* def closeEvent(self, QCloseEvent):

## Code

Example Python PyQt program :

    #библиотеки и импорты
    import sys
    #вызов библитоек
    from PyQt5.QtWidgets import (QApplication, QWidget,
                                 QToolTip, QPushButton,
                                 QMessageBox, QDesktopWidget)
    from PyQt5.QtCore import QCoreApplication
    #импортирование из либ
    from PyQt5.QtGui import QIcon
    from PyQt5.QtGui import QFont
    
    
    #Класс
    class Example(QWidget):
    
        def __init__(self):
            super().__init__()
    
            self.initUI()
    
    
        def initUI(self):
    #кнопка "файл"
            QToolTip.setFont(QFont('SansSerif', 10)) #шрифт и размер
    
            self.setToolTip('This is a <b>QWidget</b> widget')
    
            btn = QPushButton('File', self) # название кнопки
            btn.setToolTip('This is a <b>QPushButton</b> widget')
            btn.resize(btn.sizeHint())# метод sizeHint () дает рекомендумый размер кнопки
            btn.move(3, 3) #отступ кнопки от верхнего левого края
    
    #кнопка "выход"
            qbtn = QPushButton('Quit', self)
            qbtn.clicked.connect(QCoreApplication.instance().quit)
            qbtn.resize(qbtn.sizeHint())
            qbtn.move(220, 190)
    
    #запускаем приложением по центру экрана
            self.resize(300, 220)
            self.center()
            self.show()
    
    
        def center(self):
    
            qr = self.frameGeometry()#прямоугольник
            cp = QDesktopWidget().availableGeometry().center() #получаем разрещение экрана и получаем центральную точку
            qr.moveCenter(cp) #установили центр
            self.move(qr.topLeft())
    
    
    #окно
         #здесь были размеры окна   self.setGeometry(300, 300, 300, 220)  # Размер окна (относится только к окну)
            self.setWindowTitle('Teo')  # название окна
            self.setWindowIcon(QIcon('web.png'))  # рисунок иконки
    
            self.show()
    
    # всплывающее уведомление - подтверждение закрытия
    
        def closeEvent(self, QCloseEvent):
    
    
    
            reply = QMessageBox.question(self,'Message', 'Are you sure to quit?',
                                         QMessageBox.Yes | QMessageBox.No, QMessageBox.No)
    
            if reply == QMessageBox.Yes:
                QCloseEvent.accept()
            else:
                QCloseEvent.ignore()
    
    
    
    
    if __name__ == '__main__':
    
        app = QApplication(sys.argv)
        ex = Example()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
