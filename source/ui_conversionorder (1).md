---
title: ui_conversionorder (1)
date: 2020-05-07
---
Example Python program ui_conversionorder (1).py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5 import QtWebKitWidgets

## Classes

* class Ui_OrderConversion(QtWidgets.QMainWindow):

## Methods

* def setupUi(self, OrderConversion):
* def retranslateUi(self, OrderConversion):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'C:\ProgramData\Anaconda3\Library\bin\ui_orderconversion.ui'
    #
    # Created by: PyQt5 UI code generator 5.6
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_OrderConversion(QtWidgets.QMainWindow):
        def setupUi(self, OrderConversion):
            OrderConversion.setObjectName("OrderConversion")
            OrderConversion.resize(1701, 814)
            self.centralwidget = QtWidgets.QWidget(OrderConversion)
            self.centralwidget.setObjectName("centralwidget")
            self.web_view = QtWebKitWidgets.QWebView(self.centralwidget)
            self.web_view.setGeometry(QtCore.QRect(600, 19, 1091, 741))
            self.web_view.setMinimumSize(QtCore.QSize(1091, 741))
            self.web_view.setMaximumSize(QtCore.QSize(1091, 741))
            self.web_view.load(QtCore.QUrl("http://www.google.com"))
            #http://ui.anlin.com:10025/frontier/3.2.1/LoginServlet
            self.web_view.setObjectName("web_view")
            self.order_numbers = QtWidgets.QLabel(self.centralwidget)
            self.order_numbers.setGeometry(QtCore.QRect(30, 20, 91, 16))
            self.order_numbers.setObjectName("order_numbers")
            self.order_in_list_count = QtWidgets.QLabel(self.centralwidget)
            self.order_in_list_count.setGeometry(QtCore.QRect(310, 20, 91, 21))
            self.order_in_list_count.setObjectName("order_in_list_count")
            self.orders_table = QtWidgets.QTableWidget(self.centralwidget)
            self.orders_table.setGeometry(QtCore.QRect(30, 40, 551, 421))
            self.orders_table.setRowCount(1)
            self.orders_table.setColumnCount(5)
            self.orders_table.setObjectName("orders_table")
            item = QtWidgets.QTableWidgetItem()
            self.orders_table.setItem(0, 0, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.orders_table.setItem(0, 1, item)
            item = QtWidgets.QTableWidgetItem()
            item.setCheckState(QtCore.Qt.Unchecked)
            self.orders_table.setItem(0, 4, item)
            self.convert_order_si = QtWidgets.QPushButton(self.centralwidget)
            self.convert_order_si.setGeometry(QtCore.QRect(30, 470, 75, 51))
            self.convert_order_si.setObjectName("convert_order_si")
            self.print_all_orders = QtWidgets.QPushButton(self.centralwidget)
            self.print_all_orders.setGeometry(QtCore.QRect(110, 470, 75, 51))
            self.print_all_orders.setObjectName("print_all_orders")
            self.fax_all_orders = QtWidgets.QPushButton(self.centralwidget)
            self.fax_all_orders.setGeometry(QtCore.QRect(190, 470, 75, 51))
            self.fax_all_orders.setObjectName("fax_all_orders")
            self.email_all_orders = QtWidgets.QPushButton(self.centralwidget)
            self.email_all_orders.setGeometry(QtCore.QRect(270, 470, 75, 51))
            self.email_all_orders.setObjectName("email_all_orders")
            self.mixed_send_fax_email = QtWidgets.QPushButton(self.centralwidget)
            self.mixed_send_fax_email.setGeometry(QtCore.QRect(350, 470, 75, 51))
            self.mixed_send_fax_email.setObjectName("mixed_send_fax_email")
            self.clear = QtWidgets.QPushButton(self.centralwidget)
            self.clear.setGeometry(QtCore.QRect(430, 470, 151, 21))
            self.clear.setObjectName("clear")
            self.uncheck_all = QtWidgets.QPushButton(self.centralwidget)
            self.uncheck_all.setGeometry(QtCore.QRect(430, 500, 151, 21))
            self.uncheck_all.setObjectName("uncheck_all")
            OrderConversion.setCentralWidget(self.centralwidget)
    
            self.retranslateUi(OrderConversion)
            QtCore.QMetaObject.connectSlotsByName(OrderConversion)
    
        def retranslateUi(self, OrderConversion):
            _translate = QtCore.QCoreApplication.translate
            OrderConversion.setWindowTitle(_translate("OrderConversion", "MainWindow"))
            self.order_numbers.setText(_translate("OrderConversion", "Order Numbers"))
            self.order_in_list_count.setText(_translate("OrderConversion", "orders in list"))
            __sortingEnabled = self.orders_table.isSortingEnabled()
            self.orders_table.setSortingEnabled(False)
            self.orders_table.setSortingEnabled(__sortingEnabled)
            self.convert_order_si.setText(_translate("OrderConversion", "Convert \n"
    "Orders to SI"))
            self.print_all_orders.setText(_translate("OrderConversion", "Print All\n"
    " Orders"))
            self.fax_all_orders.setText(_translate("OrderConversion", "FAX All \n"
    "Orders"))
            self.email_all_orders.setText(_translate("OrderConversion", "Email All \n"
    "Orders"))
            self.mixed_send_fax_email.setText(_translate("OrderConversion", "Mixed Send \n"
    "Fax/Email"))
            self.clear.setText(_translate("OrderConversion", "Clear"))
            self.uncheck_all.setText(_translate("OrderConversion", "Uncheck All"))
    
    from PyQt5 import QtWebKitWidgets
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
