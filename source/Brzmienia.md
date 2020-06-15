---
title: Brzmienia
date: 2020-05-07
---
Example Python program Brzmienia.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import QSize, Qt, QUrl
* from PyQt5.QtGui import QIcon, QColor
* from PyQt5.QtMultimedia import QMediaPlayer, QMediaPlaylist, QMediaContent
* from PyQt5.QtWidgets import QApplication, QWidget, QLCDNumber, QSpinBox
* from PyQt5.QtWidgets import QLabel, QGridLayout
* from PyQt5.QtWidgets import QPushButton, QMessageBox
* import time
* import sys

## Classes

* class Aplikacja(QWidget):

## Methods

* def __init__(self, parent=None):
* def interfejs(self):
* def koniec(self):
* def closeEvent(self, event):
* def keyPressEvent(self, e):
* def timer(self):
* def startbtn(self):
* def againtime(self):
* def button1(self, x):
* def button2(self, x):
* def button3(self, x):
* def button4(self, x):
* def button5(self, x):
* def button6(self, x):
* def button7(self, x):
* def button8(self, x):
* def button9(self, x):
* def button10(self, x):
* def button11(self, x):
* def button12(self, x):
* def again(self, x):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    
    from PyQt5.QtCore import QSize, Qt, QUrl
    from PyQt5.QtGui import QIcon, QColor
    from PyQt5.QtMultimedia import QMediaPlayer, QMediaPlaylist, QMediaContent
    from PyQt5.QtWidgets import QApplication, QWidget, QLCDNumber, QSpinBox
    from PyQt5.QtWidgets import QLabel, QGridLayout
    from PyQt5.QtWidgets import QPushButton, QMessageBox
    
    import time
    
    
    class Aplikacja(QWidget):
        def __init__(self, parent=None):
            super().__init__(parent)
    
            self.interfejs()
            self.ended = False
            self.oncemore = False
    
        def interfejs(self):
            self.player = QMediaPlayer(self)
            self.url1 = QUrl.fromLocalFile("brzmienie-acord.wav")
            self.url2 = QUrl.fromLocalFile("brzmienie-klarnet.mp3")
            self.url3 = QUrl.fromLocalFile("brzmienie-forte.mp3")
            self.url4 = QUrl.fromLocalFile("brzmienie-kontrabas.mp3")
            self.url5 = QUrl.fromLocalFile("brzmienie-flet.mp3")
            self.url6 = QUrl.fromLocalFile("brzmienie-gitara.mp3")
            self.url7 = QUrl.fromLocalFile("brzmienie-harfa.mp3")
            self.url8 = QUrl.fromLocalFile("brzmienie-waltornia.mp3")
            self.url9 = QUrl.fromLocalFile("brzmienie-saksofon.mp3")
            self.url10 = QUrl.fromLocalFile("brzmienie-trabka.mp3")
            self.url11 = QUrl.fromLocalFile("brzmienie-skrzypce.mp3")
            self.url12 = QUrl.fromLocalFile("brzmienie-tuba.mp3")
    
            self.s1 = QMediaContent(self.url1)
            self.s2 = QMediaContent(self.url2)
            self.s3 = QMediaContent(self.url3)
            self.s4 = QMediaContent(self.url4)
            self.s5 = QMediaContent(self.url5)
            self.s6 = QMediaContent(self.url6)
            self.s7 = QMediaContent(self.url7)
            self.s8 = QMediaContent(self.url8)
            self.s9 = QMediaContent(self.url9)
            self.s10 = QMediaContent(self.url10)
            self.s11 = QMediaContent(self.url11)
            self.s12 = QMediaContent(self.url12)
    
            self.playlist = QMediaPlaylist(self)
            self.playlist.addMedia(self.s1)
            self.playlist.addMedia(self.s2)
            self.playlist.addMedia(self.s3)
            self.playlist.addMedia(self.s4)
            self.playlist.addMedia(self.s5)
            self.playlist.addMedia(self.s6)
            self.playlist.addMedia(self.s7)
            self.playlist.addMedia(self.s8)
            self.playlist.addMedia(self.s9)
            self.playlist.addMedia(self.s10)
            self.playlist.addMedia(self.s11)
            self.playlist.addMedia(self.s12)
    
            self.playlist.setPlaybackMode(QMediaPlaylist.Loop)
            self.playlist.shuffle()
    
            self.player.setPlaylist(self.playlist)
    
            self.Btn1 = QPushButton(self)
            Icn1 = QIcon('acord.png')
            self.Btn1.setIcon(Icn1)
            self.Btn1.setIconSize(QSize(160, 240))
    
            self.Btn2 = QPushButton(self)
            Icn2 = QIcon('clarinet.png')
            self.Btn2.setIcon(Icn2)
            self.Btn2.setIconSize(QSize(160, 240))
    
            self.Btn3 = QPushButton(self)
            Icn3 = QIcon('forte.png')
            self.Btn3.setIcon(Icn3)
            self.Btn3.setIconSize(QSize(160, 240))
    
            self.Btn4 = QPushButton(self)
            Icn4 = QIcon('double-bass.png')
            self.Btn4.setIcon(Icn4)
            self.Btn4.setIconSize(QSize(160,240))
    
            self.Btn5 = QPushButton(self)
            Icn5 = QIcon('flute1.png')
            self.Btn5.setIcon(Icn5)
            self.Btn5.setIconSize(QSize(160,240))
    
            self.Btn6 = QPushButton(self)
            Icn6 = QIcon('gitara.bmp kopia.png')
            self.Btn6.setIcon(Icn6)
            self.Btn6.setIconSize(QSize(160, 240))
    
            self.Btn7 = QPushButton(self)
            Icn7 = QIcon('harp.png')
            self.Btn7.setIcon(Icn7)
            self.Btn7.setIconSize(QSize(160, 240))
    
            self.Btn8 = QPushButton(self)
            Icn8 = QIcon('horn.png')
            self.Btn8.setIcon(Icn8)
            self.Btn8.setIconSize(QSize(160, 240))
    
            self.Btn9 = QPushButton(self)
            Icn9 =QIcon('saksofon1.png')
            self.Btn9.setIcon(Icn9)
            self.Btn9.setIconSize(QSize(160, 240))
    
            self.Btn10 = QPushButton(self)
            Icn10 = QIcon('trumpet.png')
            self.Btn10.setIcon(Icn10)
            self.Btn10.setIconSize(QSize(160, 240))
    
            self.Btn11 = QPushButton(self)
            Icn11 = QIcon('violin1.png')
            self.Btn11.setIcon(Icn11)
            self.Btn11.setIconSize(QSize(160, 240))
    
            self.Btn12 = QPushButton(self)
            Icn12 = QIcon('tuba.png')
            self.Btn12.setIcon(Icn12)
            self.Btn12.setIconSize(QSize(160, 240))
    
            self.koniecBtn = QPushButton("&Koniec", self)
            self.jeszczerazBtn = QPushButton ("Jeszcze raz", self)
            self.koniecBtn.resize(self.koniecBtn.sizeHint())
            self.jeszczerazBtn.resize(self.jeszczerazBtn.sizeHint())
            self.startBtn = QPushButton("Start", self)
    
            playBtn = QPushButton(self)
            Icn13 = QIcon('play.png')
            playBtn.setIcon(Icn13)
            playBtn.setIconSize(QSize(30, 30))
    
            stopBtn = QPushButton(self)
            Icn14 = QIcon('pause.png')
            stopBtn.setIcon(Icn14)
            stopBtn.setIconSize(QSize(30, 30))
    
            nextBtn = QPushButton(self)
            Icn15 = QIcon('forward.png')
            nextBtn.setIcon(Icn15)
            nextBtn.setIconSize(QSize(30, 30))
    
            Good = QLabel("Dobrze:", self)
            self.GoodEdt = QLCDNumber()
            self.GoodEdt.setSegmentStyle(QLCDNumber.Flat)
            self.GoodEdt.setDecMode()
            self.GoodEdt.intValue()
    
            Wrong = QLabel("Żle:", self)
            self.WrongEdt = QLCDNumber()
            self.WrongEdt.setSegmentStyle(QLCDNumber.Flat)
            self.WrongEdt.setDecMode()
    
            Sum = QLabel("Razem", self)
            self.SumEdt = QLCDNumber()
            self.SumEdt.setSegmentStyle(QLCDNumber.Flat)
            self.SumEdt.setDecMode()
    
            Timer = QLabel("Czas:", self)
            self.TimeEdt = QLCDNumber()
            self.TimeEdt.setSegmentStyle(QLCDNumber.Flat)
            self.TimeEdt.setDecMode()
    
            palette1 = self.TimeEdt.palette()
            palette1.setColor(palette1.WindowText, QColor(85, 85, 255))
            self.TimeEdt.setPalette(palette1)
    
            self.pallete2 = self.GoodEdt.palette()
            self.pallete2.setColor(self.pallete2.WindowText, QColor(0, 255, 0))
            self.GoodEdt.setPalette(self.pallete2)
    
            pallete3 = self.WrongEdt.palette()
            pallete3.setColor(pallete3.WindowText, QColor(255, 0, 0))
            self.WrongEdt.setPalette(pallete3)
    
            self.spinbox = QSpinBox(self)
            self.spinbox.setValue(30)
    
            self.ukladT = QGridLayout(self)
    
            self.ukladT.addWidget(self.Btn1, 1, 1)
            self.ukladT.addWidget(self.Btn2, 1, 2)
            self.ukladT.addWidget(self.Btn3, 1, 3)
            self.ukladT.addWidget(self.Btn4, 1, 4)
            self.ukladT.addWidget(self.Btn5, 1, 5)
            self.ukladT.addWidget(self.Btn6, 1, 6)
            self.ukladT.addWidget(self.Btn7, 3, 1)
            self.ukladT.addWidget(self.Btn8, 3, 2)
            self.ukladT.addWidget(self.Btn9, 3, 3)
            self.ukladT.addWidget(self.Btn10, 3, 4)
            self.ukladT.addWidget(self.Btn11, 3, 5)
            self.ukladT.addWidget(self.Btn12, 3, 6)
    
            self.ukladT.addLayout(self.ukladT, 0, 0, 0, 0)
            self.ukladT.addWidget(Good,5, 1, 1, 3)
            self.ukladT.addWidget(Wrong,5, 2, 1, 3)
            self.ukladT.addWidget(Sum, 5, 3, 1, 3)
            self.ukladT.addWidget(Timer, 6, 5, 1, 3)
            self.ukladT.addWidget(self.GoodEdt, 6, 1, 2, 1)
            self.ukladT.addWidget(self.WrongEdt, 6, 2, 2, 1)
            self.ukladT.addWidget(self.SumEdt, 6, 3, 2, 1)
            self.ukladT.addWidget(self.TimeEdt,6, 6, 2, 1)
            self.ukladT.addWidget(self.spinbox, 6, 5, 2, 1)
            self.ukladT.addWidget(playBtn, 4, 1, 1, 2)
            self.ukladT.addWidget(stopBtn, 4, 3, 1, 2)
            self.ukladT.addWidget(nextBtn, 4, 5, 1, 2)
            self.ukladT.addWidget(self.startBtn, 8, 3, 2, 2)
            self.ukladT.addWidget(self.jeszczerazBtn, 8, 0, 2, 2)
            self.ukladT.addWidget(self.koniecBtn, 8, 6, 2, 2)
    
            self.setLayout(self.ukladT)
            self.setGeometry(150, 20, 500, 500)
            self.setWindowIcon(QIcon('nuta.png'))
            self.setWindowTitle("Brzmienia")
            self.show()
    
            playBtn.clicked.connect(self.player.play)
    
            stopBtn.clicked.connect(self.player.pause)
    
            nextBtn.clicked.connect(self.playlist.next)
            nextBtn.clicked.connect(self.player.play)
    
            self.koniecBtn.clicked.connect(self.player.pause)
            self.koniecBtn.clicked.connect(self.koniec)
    
            self.jeszczerazBtn.clicked.connect(self.player.stop)
            self.jeszczerazBtn.clicked.connect(self.again)
            self.jeszczerazBtn.clicked.connect(self.againtime)
    
            self.startBtn.clicked.connect(self.startbtn)
            self.startBtn.clicked.connect(self.player.play)
            self.startBtn.clicked.connect(self.timer)
    
            self.Btn1.clicked.connect(self.button1)
            self.Btn1.clicked.connect(self.playlist.next)
    
            self.Btn2.clicked.connect(self.button2)
            self.Btn2.clicked.connect(self.playlist.next)
    
            self.Btn3.clicked.connect(self.button3)
            self.Btn3.clicked.connect(self.playlist.next)
    
            self.Btn4.clicked.connect(self.button4)
            self.Btn4.clicked.connect(self.playlist.next)
    
            self.Btn5.clicked.connect(self.button5)
            self.Btn5.clicked.connect(self.playlist.next)
    
            self.Btn6.clicked.connect(self.button6)
            self.Btn6.clicked.connect(self.playlist.next)
    
            self.Btn7.clicked.connect(self.button7)
            self.Btn7.clicked.connect(self.playlist.next)
    
            self.Btn8.clicked.connect(self.button8)
            self.Btn8.clicked.connect(self.playlist.next)
    
            self.Btn9.clicked.connect(self.button9)
            self.Btn9.clicked.connect(self.playlist.next)
    
            self.Btn10.clicked.connect(self.button10)
            self.Btn10.clicked.connect(self.playlist.next)
    
            self.Btn11.clicked.connect(self.button11)
            self.Btn11.clicked.connect(self.playlist.next)
    
            self.Btn12.clicked.connect(self.button12)
            self.Btn12.clicked.connect(self.playlist.next)
    
            self.spinbox2 = QSpinBox(self)
            self.spinbox2.setValue(0)
    
            self.resize(1100, 700)
            self.showFullScreen()
            self.setWindowTitle("Aplikacja")
            self.show()
    
        def koniec(self):
                self.ended = True
                self.close()
    
        def closeEvent(self, event):
    
            odp = QMessageBox.question(self, 'Komunikat', "Czy na pewno koniec?",
                QMessageBox.Yes | QMessageBox.No, QMessageBox.No)
    
            if odp == QMessageBox.Yes:
                event.accept()
    
            else:
                event.ignore()
    
        def keyPressEvent(self, e):
            if e.key() == Qt.Key_Escape:
                self.close()
    
        def timer(self):
    
            for tick in range(self.spinbox.value(), -1, -1):
                self.TimeEdt.display(tick)
                self.startBtn.setEnabled(not tick)
                start = time.time()
                while time.time() - start < 1:
                    app.processEvents()
                if tick == 0:
                    self.player.pause()
                    self.stop = QMessageBox.warning(self, "Niestety!", "Koniec czasu!")
                if self.ended:
                    break
                if self.oncemore:
                    break
    
        def startbtn(self):
            self.oncemore = False
    
        def againtime(self):
    
            for tick in range(self.spinbox.value(), -1, -1):
                self.TimeEdt.display(tick)
                self.startBtn.setEnabled(not tick)
                self.oncemore = True
    
        def button1(self, x):
            y = self.playlist.currentMedia()
            if y == self.s1:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn1.setDisabled(x)
    
            if not y == self.s1:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button2(self, x):
            y = self.playlist.currentMedia()
            if y == self.s2:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn2.setDisabled(x)
            if not y == self.s2:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button3(self, x):
            y = self.playlist.currentMedia()
            if y == self.s3:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn3.setDisabled(x)
            if not y == self.s3:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button4(self, x):
            y = self.playlist.currentMedia()
            if y == self.s4:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn4.setDisabled(x)
            if not y == self.s4:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button5(self, x):
            y = self.playlist.currentMedia()
            if y == self.s5:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn5.setDisabled(x)
            if not y == self.s5:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button6(self, x):
            y = self.playlist.currentMedia()
            if y == self.s6:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn6.setDisabled(x)
            if not y == self.s6:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button7(self, x):
            y = self.playlist.currentMedia()
            if y == self.s7:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn7.setDisabled(x)
            if not y == self.s7:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button8(self, x):
            y = self.playlist.currentMedia()
            if y == self.s8:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn8.setDisabled(x)
            if not y == self.s8:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button9(self, x):
            y = self.playlist.currentMedia()
            if y == self.s9:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn9.setDisabled(x)
            if not y == self.s9:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button10(self, x):
            y = self.playlist.currentMedia()
            if y == self.s10:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn10.setDisabled(x)
            if not y == self.s10:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button11(self, x):
            y = self.playlist.currentMedia()
            if y == self.s11:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn11.setDisabled(x)
            if not y == self.s11:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def button12(self, x):
            y = self.playlist.currentMedia()
            if y == self.s12:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.GoodEdt.value()
                    self.GoodEdt.display(i + 1)
                self.Btn12.setDisabled(x)
            if not y == self.s12:
                for i in range(self.spinbox2.value(), +1, +1):
                    i = self.WrongEdt.value()
                    self.WrongEdt.display(i + 1)
                    self.wrong = QMessageBox.critical(self, "Źle", "Źle")
            z = self.SumEdt.value()
            self.SumEdt.display(z + 1)
    
        def again(self, x):
                x = 0
                self.Btn1.setDisabled(x)
                self.Btn2.setDisabled(x)
                self.Btn3.setDisabled(x)
                self.Btn4.setDisabled(x)
                self.Btn5.setDisabled(x)
                self.Btn6.setDisabled(x)
                self.Btn7.setDisabled(x)
                self.Btn8.setDisabled(x)
                self.Btn9.setDisabled(x)
                self.Btn10.setDisabled(x)
                self.Btn11.setDisabled(x)
                self.Btn12.setDisabled(x)
                self.GoodEdt.display(x)
                self.WrongEdt.display(x)
                self.SumEdt.display(x)
                self.oncemore = True
                self.playlist.shuffle()
    
    
    if __name__ == '__main__':
        import sys
    
        app = QApplication(sys.argv)
        okno = Aplikacja()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
