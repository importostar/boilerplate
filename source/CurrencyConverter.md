---
title: CurrencyConverter
date: 2020-05-07
---
Example Python program CurrencyConverter.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from datetime import datetime
* import calendar
* from PyQt5.QtCore import QDate
* from PyQt5.QtGui import QIcon
* from urllib.request import urlopen, urlretrieve
* from decimal import Decimal
* from PyQt5.QtWidgets import QCalendarWidget, QWidget, QLabel, QComboBox, QDoubleSpinBox, QMessageBox, QApplication, \
* from PyQt5.QtGui import QIcon, QPixmap
* from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
* from PyQt5.QtCore import QUrl
* from fixerio import Fixerio
* import requests
* import json
* # graph import
* import pyqtgraph as pg
* import pyqtgraph.exporters
* import numpy as np

## Classes

* class Calendar(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* # def calculator(self):
* def printDateInfo(self, qDate):
* def closeEvent(self, event):
* def fixer(self):
* def conversionShow(self):
* def set_window_icon_from_response(self, http_response):
* def main():

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    """
    Created on Mon Sep 30 10:07:39 2019
    """
    
    import sys
    from datetime import datetime
    import calendar
    from PyQt5.QtCore import QDate
    from PyQt5.QtGui import QIcon
    from urllib.request import urlopen, urlretrieve
    from decimal import Decimal
    from PyQt5.QtWidgets import QCalendarWidget, QWidget, QLabel, QComboBox, QDoubleSpinBox, QMessageBox, QApplication, \
        QGridLayout, QLineEdit, QPushButton
    
    from PyQt5.QtGui import QIcon, QPixmap
    from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
    from PyQt5.QtCore import QUrl
    
    from fixerio import Fixerio
    import requests
    import json
    
    # graph import
    import pyqtgraph as pg
    import pyqtgraph.exporters
    import numpy as np
    
    
    class Calendar(QWidget):
        global currentYear, currentMonth
    
        currentMonth = datetime.now().month
        currentYear = datetime.now().year
    
        def __init__(self):
            super().__init__()
            self.setWindowTitle('Calendar')
            self.setGeometry(300, 300, 940, 600)
            self.initUI()
            self.fixer()
    
            ICON_IMAGE_URL = "https://www.google.ge/images/branding/product/ico/googleg_lodp.ico"
            self.nam = QNetworkAccessManager()
            self.nam.finished.connect(self.set_window_icon_from_response)
            self.nam.get(QNetworkRequest(QUrl(ICON_IMAGE_URL)))
    
        # self.setWindowIcon(QIcon('icon.png'))
    
        def initUI(self):
    
            # First Calendar - START
            self.calendar = QCalendarWidget(self)
            self.calendar.move(35, 150)
            self.calendar.setGridVisible(True)
    
            self.calendar.setMinimumDate(QDate(currentYear, currentMonth - 2, 1))
            self.calendar.setMaximumDate(
                QDate(currentYear, currentMonth + 3, calendar.monthrange(currentYear, currentMonth)[1]))
            self.calendar.setSelectedDate(QDate(currentYear, currentMonth, 1))
            self.calendar.clicked.connect(self.printDateInfo)
            # First Calendar - END
    
            # Second Calendar - START
    
            self.calendarSecond = QCalendarWidget(self)
            self.calendarSecond.move(500, 150)
            self.calendarSecond.setGridVisible(True)
    
            self.calendarSecond.setMinimumDate(QDate(currentYear, currentMonth - 2, 1))
            self.calendarSecond.setMaximumDate(
                QDate(currentYear, currentMonth + 3, calendar.monthrange(currentYear, currentMonth)[1]))
            self.calendarSecond.setSelectedDate(QDate(currentYear, currentMonth + 1, 1))
            self.calendarSecond.clicked.connect(self.printDateInfo)
            # Second Calender - END
    
            # Currency Converter - START
    
            # Input side - START
            self.fromInput = QLabel(self)
            self.fromInput.setText("Select Currency:")
            self.fromInput.setStyleSheet('font: 10pt')
            self.fromInput.move(45, 20)
    
            self.fromComboBox = QComboBox(self)
            self.fromComboBox.addItem('           ')
            self.fromComboBox.addItem('€ - Euro')
            self.fromComboBox.addItem('£ - GPB')
            self.fromComboBox.addItem('$ - US Dollars')
            self.fromComboBox.move(210, 20)
            self.fromComboBox.resize(200, 25)
            self.fromComboBox.setStyleSheet('font: 9pt ')
    
            self.amountInput = QLabel(self)
            self.amountInput.setText('Amount to convert: ')
            self.amountInput.setStyleSheet('font: 10pt ')
            self.amountInput.move(45, 55)
    
            self.convertInput = QDoubleSpinBox(self)
            self.convertInput.setRange(0, 100000)
            self.convertInput.move(210, 55)
            self.convertInput.setStyleSheet('font: 9pt')
            # Input Side - END
    
            # Output side - START
            self.fromOutput = QLabel(self)
            self.fromOutput.setText("Select Currency:")
            self.fromOutput.setStyleSheet('font: 10pt')
            self.fromOutput.move(515, 20)
    
            self.amountOutput = QLabel(self)
            self.amountOutput.setText('Result: ')
            self.amountOutput.setStyleSheet('font: 10pt ')
            self.amountOutput.move(515, 55)
    
            self.convertOutput = QLineEdit(self)
            self.convertOutput.move(650, 55)
            self.convertOutput.resize(125, 25)
            self.convertOutput.setStyleSheet('font: 10pt ')
            self.convertOutput.setReadOnly(True)
    
    
            self.toComboBox = QComboBox(self)
            self.toComboBox.addItem('           ')
            self.toComboBox.addItem('€ - Euro')
            self.toComboBox.addItem('£ - GPB')
            self.toComboBox.addItem('$ - US Dollars')
            self.toComboBox.move(650, 20)
            self.toComboBox.resize(200, 25)
            self.toComboBox.setStyleSheet('font: 9pt ')
    
            # Output side - END
    
            # GRAPH - START
            # redundent //TODO ?
            # GRAPH - END
    
            # Currency Converter - END
    
            self.btn = QPushButton("Submit", self)
            self.btn.resize(60, 45)
            self.btn.move(50, 90)
            self.btn.setStyleSheet("QPushButton {background-color: #DCDCDC }"
                                   "QPushButton:pressed { background-color: #F5F5F5 }")
    
            self.btn.clicked.connect(self.conversionShow)
    
        # def calculator(self):
    
        def printDateInfo(self, qDate):
            print('{0}/{1}/{2}'.format(qDate.month(), qDate.day(), qDate.year()))
            print(f'Day Number of the year: {qDate.dayOfYear()}')
            print(f'Day Number of the week: {qDate.dayOfWeek()}')
    
        # Close Event - START
        def closeEvent(self, event):
    
            reply = QMessageBox.question(self, 'Message',
                                         "Are you sure to quit?", QMessageBox.Yes |
                                         QMessageBox.No, QMessageBox.No)
    
            if reply == QMessageBox.Yes:
                event.accept()
            else:
                event.ignore()
    
        # Close Event - END
    
        # Import Currency & API - START
    
        # fixer API
        # url = "http://data.fixer.io/api/latest?access_key=" + access_key
        # response = requests.get(url)
        # data = response.text
    
        def fixer(self):
    
            #fixer.io access key
            access_key = "67e6a4813e5cfce6a30b0b0ac6a4003c"
            url = "http://data.fixer.io/api/latest?access_key=" + access_key
            response = requests.get(url)
            data = response.text
            # print only for development / debugging purpose
            #print(data)
            parsed = json.loads(data)
    
            #print only for development / debugging purpose
            #print(json.dumps(parsed, indent=4))
    
            date = parsed["date"]
            #print(date)
            self.gbp_rate = round(parsed["rates"]["GBP"], 2)
            self.usd_rate = round(parsed["rates"]["USD"], 2)
            self.eur_rate = 1.00
    
            #print(self.gbp_rate)
            #print(self.usd_rate)
    
    
            #ConvRate - Display - START
            self.convRateLabel = QLabel(self)
            self.convRateLabel.setText("Conversion Rate                             Base €:")
            self.convRateLabel.setStyleSheet("font: 10pt")
            self.convRateLabel.move(515, 85)
    
            self.convRate = QLineEdit(self)
            self.convRate.move(650, 85)
            self.convRate.resize(125, 25)
            self.convRate.setStyleSheet('font: 10pt; background-color: #c9cbd0; ')
            self.convRate.setReadOnly(True)
            # ConvRate - Display - END
    
            # Import Currency & API - END
    
        #conversion - START (and display in relevant boxes)
        def conversionShow(self):
    
            #replacing floating numbers with rounded values
            GBPtoEUR = round(self.convertInput.value() / self.gbp_rate, 4)
            GBPtoUSD = round((self.convertInput.value() / self.gbp_rate) * self.usd_rate, 4)
            GBPtoGBP = round((self.convertInput.value() / self.gbp_rate) * self.gbp_rate, 4)
    
            USDtoEUR = round(self.convertInput.value() / self.eur_rate, 4)
            USDtoGBP = round((self.convertInput.value() / self.usd_rate) * self.gbp_rate, 4)
            USDtoUSD = round((self.convertInput.value() / self.usd_rate) * self.usd_rate, 4)
    
            EURtoGBP = round((self.convertInput.value() * self.gbp_rate), 4)
            EURtoUSD = round((self.convertInput.value() * self.usd_rate), 4)
            EURtoEUR = round((self.convertInput.value() * self.eur_rate), 4)
    
    
            # EUR to GBP conversion
            if str(self.fromComboBox.currentText()) == '€ - Euro' and str(self.toComboBox.currentText()) == '€ - Euro':
                self.convertOutput.setText(str(EURtoEUR))
                self.convRate.setText(str(1))
            # GBP to EUR conversion
            elif str(self.fromComboBox.currentText()) == '£ - GPB' and str(self.toComboBox.currentText()) == '€ - Euro':
                self.convertOutput.setText(str(GBPtoEUR))
                self.convRate.setText(str(self.gbp_rate))
            # USD to EURO conversion
            elif str(self.fromComboBox.currentText()) == '$ - US Dollars' and str(
                    self.toComboBox.currentText()) == '€ - Euro':
                self.convertOutput.setText(str(USDtoEUR))
                self.convRate.setText(str(self.usd_rate))
            #   EUR to GBP conversion
            elif str(self.fromComboBox.currentText()) == '€ - Euro' and str(self.toComboBox.currentText()) == '£ - GPB':
                self.convertOutput.setText(str(EURtoGBP))
                self.convRate.setText(str(self.gbp_rate))
            # GBP to GBP conversion
            elif str(self.fromComboBox.currentText()) == '£ - GPB' and str(self.toComboBox.currentText()) == '£ - GPB':
                self.convertOutput.setText(str(GBPtoGBP))
                self.convRate.setText(str(1))
            # USD to GBP conversion
            elif str(self.fromComboBox.currentText()) == '$ - US Dollars' and str(
                    self.toComboBox.currentText()) == '£ - GPB':
                self.convertOutput.setText(str(USDtoGBP))
                self.convRate.setText(str(self.usd_rate))
            # EUR to USD conversion
            elif str(self.fromComboBox.currentText()) == '€ - Euro' and str(
                    self.toComboBox.currentText()) == '$ - US Dollars':
                self.convertOutput.setText(str(EURtoUSD))
                self.convRate.setText(str(self.usd_rate))
            # GBP to USD conversion
            elif str(self.fromComboBox.currentText()) == '£ - GPB' and str(
                    self.toComboBox.currentText()) == '$ - US Dollars':
                self.convertOutput.setText(str(GBPtoUSD))
                self.convRate.setText(str(self.gbp_rate))
            # USd to USD conversion
            elif str(self.fromComboBox.currentText()) == '$ - US Dollars' and str(
                    self.toComboBox.currentText()) == '$ - US Dollars':
                self.convertOutput.setText(str(USDtoUSD))
                self.convRate.setText(str(self.usd_rate))
        #conversion - END
    
        #QIcon - Start
    
    
        def set_window_icon_from_response(self, http_response):
            pixmap = QPixmap()
            pixmap.loadFromData(http_response.readAll())
            icon = QIcon(pixmap)
            self.setWindowIcon(icon)
    
        #QIcon - End
    
    def main():
        app = QApplication(sys.argv)
        cal = Calendar()
        cal.show()
        sys.exit(app.exec_())
    
    
    main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
