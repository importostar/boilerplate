---
title: mian_page006
date: 2020-05-07
---
Example Python program mian_page006.py
This program creates a PyQt GUI

## Modules

* import sys
* import time
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import QIcon,QBrush,QColor,QStandardItemModel,QStandardItem
* from PyQt5.QtCore import QThread,pyqtSignal,QDateTime

## Classes

* class BasicTableView(QTableView):
* class BackendThread(QThread):
* class ThreadUpdateUI(QDialog):

## Methods

* def __init__(self):
* def show_data(self, rows: list, column_names: list):
* def init_UI(self):
* def handelDisplay(self,data):
* def run(self):
* def __init__(self):
* def initUI(self):
* def handleDisplay(self,data):

## Code

Example Python PyQt program :

    '''
    1、数据查找模块的编写
    2、多线程更新UI数据
    '''
    
    import sys
    import time
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import QIcon,QBrush,QColor,QStandardItemModel,QStandardItem
    from PyQt5.QtCore import QThread,pyqtSignal,QDateTime
    
    
    class BasicTableView(QTableView):
        def __init__(self):
            super().__init__()
            ##必须放在初始化时，赋值及定义，放在show_data方法中有问题，不能动态的改变属性，
            # 而QStandardItemModel的clear会直接动态的删除Model的数据，view也就没有了
    
    
            self._row_number=10000
            self._column_number=3
            self._current_row=0
    
    
            self.model = QStandardItemModel(self._row_number, self._column_number)
    
            self.init_UI()
    
        def show_data(self, rows: list, column_names: list):
            self.model.setRowCount(len(rows))
            self.model.setColumnCount(len(column_names))
            self.model.setHorizontalHeaderLabels(column_names)
    
            self.tableview = QTableView()
            # 关联QTableView和Model
            self.tableview.setModel(self.model)
    
            self.tableview.horizontalHeader().setStretchLastSection(True)
            # self.tableview.horizontalHeader().setSectionResizeMode(QHeaderView.Stretch)
            self.tableview.setEditTriggers(QAbstractItemView.NoEditTriggers)  # 不可编辑
            self.tableview.setSelectionMode(QAbstractItemView.SingleSelection)  # 设置只能选中一行
            self.tableview.setSelectionBehavior(QAbstractItemView.SelectRows)  # 设置只有行选中
    
            # 添加数据
            for num0, item0 in enumerate(rows):
                for num1, item1 in enumerate(item0):
                    qstd_item = QStandardItem(item1)
                    if 'NG' in item0:
                        # qstd_item.setBackground(QBrush(QColor(255,255,0)))
                        qstd_item.setBackground(QBrush(QColor(255, 102, 102)))
                    else:
                        qstd_item.setBackground(QBrush(QColor(153, 204, 102)))
                    self.model.setItem(num0, num1, qstd_item)
    
    
    
            # 样式
            layout = QVBoxLayout()
            layout.addWidget(self.tableview)
            self.setLayout(layout)
    
    
    
        def init_UI(self):
            self.tableview = QTableView()
            self.tableview.setModel(self.model)
            self.tableview.horizontalHeader().setStretchLastSection(True)
    
            layout = QVBoxLayout()
            layout.addWidget(self.tableview)
            self.setLayout(layout)
    
            self.backend=BackendThread()
            self.backend.update_date.connect(self.handelDisplay)
    
            self.backend.start()
    
    
    
        def handelDisplay(self,data):
    
    
    
            if self._current_row<self._row_number:
                for i in range(self._column_number):
                    self.model.setItem(self._current_row, i, QStandardItem(data))
                self._current_row = self._current_row + 1
            else:
                self.backend.is_stop = True
    
    
    
    
    
    
    
    
    class BackendThread(QThread):
        update_date=pyqtSignal(str)
        is_stop=False
    
        def run(self):
            while True:
                if self.is_stop:
                    break
                data = QDateTime.currentDateTime()
                currentTime = data.toString("yyyy-MM-dd hh:mm:ss")
                self.update_date.emit(str(currentTime))
                time.sleep(0.0000009)
    
    
    
    class ThreadUpdateUI(QDialog):
    
        def __init__(self):
            QDialog.__init__(self)
            self.setWindowTitle('多线程更新UI数据')
            self.resize(400,100)
            self.input=QTextEdit(self)
            self.input.resize(400,100)
    
    
            self.initUI()
    
        def initUI(self):
            self.backend=BackendThread()
            self.backend.update_date.connect(self.handleDisplay)
    
            self.backend.start()
    
        def handleDisplay(self,data):
            self.input.setText(data)
    
    
    
    
    if __name__=="__main__":
        app=QApplication(sys.argv)
        example=BasicTableView()
    
        example.show()
    
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
