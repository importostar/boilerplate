---
title: covid 19 tr
date: 2020-05-07
---
Example Python program covid-19-tr.py
This program creates a PyQt GUI

## Modules

* from bs4 import BeautifulSoup
* import requests
* from PyQt5.QtWidgets import QApplication, QLabel, QWidget, QListWidget, QVBoxLayout, QGroupBox, QGroupBox, QHBoxLayout, QSplitter
* from PyQt5.QtCore import QTimer, Qt
* import sys

## Classes

* class Window(QWidget):

## Methods

* def __init__(self):
* def setUI(self):
* def addData(self):
* def getData(self):

## Code

Example Python PyQt program :

    from bs4 import BeautifulSoup
    import requests
    from PyQt5.QtWidgets import QApplication, QLabel, QWidget, QListWidget, QVBoxLayout, QGroupBox, QGroupBox, QHBoxLayout, QSplitter
    from PyQt5.QtCore import QTimer, Qt
    import sys
    
    class Window(QWidget):
        def __init__(self):
            super(Window, self).__init__()
            self.setUI()
    
        def setUI(self):
            self.listWidget1 = QListWidget()
            self.listWidget2 = QListWidget()
            self.groupBox = QGroupBox()
    
            h_box = QHBoxLayout()
            splitter = QSplitter(Qt.Horizontal)
            splitter.addWidget(self.listWidget1)
            splitter.addWidget(self.listWidget2)
            h_box.addWidget(splitter)
            self.groupBox.setLayout(h_box)
    
            self.addData()
    
            v_box = QVBoxLayout()
            v_box.addWidget(self.groupBox)
    
            self.setLayout(v_box)
            self.setWindowTitle(self.getData()[0].title.text)
            self.setFixedSize(600, 400)
    
            self.timer = QTimer()
            self.timer.timeout.connect(self.addData)
            self.timer.start(5*60000)
    
        def addData(self):
            self.listWidget1.clear()
            self.listWidget2.clear()
            self.groupBox.setTitle(self.getData()[2])
            texts = ["Toplam test sayısı", "Toplam vaka sayısı", "Toplam vefat sayısı", "Toplam yoğun bakım hasta sayısı",
                     "Toplam entube hasta sayısı", "Toplam iyileşen hasta sayısı", "Bugünkü test sayısı", "Bugünkü vaka sayısı",
                     "Bugünkü vefat sayısı", "Bugünkü iyileşen sayısı"]
            for i in texts:
                self.listWidget1.addItem(i)
            for i in range(10):
                self.listWidget2.addItem(self.getData()[1][i])
    
        def getData(self):                
            r = requests.get("https://covid19.saglik.gov.tr")
            soup = BeautifulSoup(r.content, "html.parser")
    
            date = []
            for i in soup.find_all("p"):
                date.append(i.text)
            date_str = date[1] + " " + date[2] + " " + date[3]
    
            data = []
            for i in soup.find_all("span"):
                j = i.text.split()[0].replace(".", "")
                try: int(j)
                except ValueError: continue
                data.append(j)
    
            return soup, data, date_str
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        window = Window()
        window.show()
        sys.exit(app.exec())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
