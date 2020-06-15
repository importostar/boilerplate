---
title: put_grate_into_put_grate_into (1)
date: 2020-05-07
---
Example Python program put_grate_into.py_put_grate_into (1).py
This program creates a PyQt GUI

## Modules

* from PyQt5 import  QtWidgets
* from untitled import  Ui_Dialog
* from PyQt5.QtWidgets import *
* import pandas as pd
* import numpy as np
* from PyQt5.QtCore import *
* from openpyxl import load_workbook
* from openpyxl.utils import get_column_letter
* import sys

## Classes

* class mywindow(QtWidgets.QWidget,Ui_Dialog):

## Methods

* def __init__(self) :
* def openfile(self):
* def creat_table_show(self):
* def table_insert(self):
* def table_update(self):
* def table_delete(self):
* def save_table(self):
* def number_find(self):
* def name_find(self):
* def text_changed(self,text):
* def selectionchange(self):
* def selectionchange_0(self):
* def no_grates(self):

## Code

Example Python PyQt program :

    from PyQt5 import  QtWidgets
    from untitled import  Ui_Dialog
    from PyQt5.QtWidgets import *
    import pandas as pd
    import numpy as np
    from PyQt5.QtCore import *
    from openpyxl import load_workbook
    from openpyxl.utils import get_column_letter
    
    
    #=====================对象创建，按钮链接======================
    class mywindow(QtWidgets.QWidget,Ui_Dialog):
        def __init__(self) :
            super(mywindow,self).__init__()
            self.setupUi(self)
            self.pushButton.clicked.connect(self.openfile)
            self.pushButton.clicked.connect(self.creat_table_show)
            self.lineEdit.textChanged.connect(self.text_changed)
            self.pushButton_2.clicked.connect(self.name_find)
            self.pushButton_3.clicked.connect(self.number_find)
            self.pushButton_4.clicked.connect(self.creat_table_show)
            self.pushButton_5.clicked.connect(self.no_grates)
            self.pushButton_6.clicked.connect(self.save_table)
            self.tableWidget.itemChanged.connect(self.table_update)
            self.label_2.setText("有0条结果")#标签
    
            information_0=["实验老师","张岷涛","杨帆","罗晖","魏东"]
            self.comboBox.addItems(information_0)
            information_1=["实验项目","RC一阶电路的响应测试","R、L、C串联谐振电路的研究","戴维南定理","电路元件伏安特性的测绘","电压源与电流源的等效变换","叠加原理的验证","二阶动态电路响应的研究","三相交流电源电压、电流的测量","实验考试","用三表法测量电路等效参数","正弦稳压交流电路相量的研究"]
            self.comboBox_2.addItems(information_1)
            self.comboBox.currentIndexChanged.connect(self.selectionchange)
            self.comboBox_2.currentIndexChanged.connect(self.selectionchange_0)
    
    #===============打开文件并获取路径===========================
        def openfile(self):
    
            openfile_name =QFileDialog.getOpenFileName(self,
                                                            "选取文件",
                                                            "c:/ ",
                                                            "All Files(*);;Excel files( *.xlsx)"
                                                            )
    
    
            global path_openfile_name
            path_openfile_name = openfile_name[0]
    
    #================读取eccel文件并显示==========================
        def creat_table_show(self):
            if len(path_openfile_name) > 0:
                input_table = pd.read_excel(path_openfile_name)
                input_table_rows = input_table.shape[0]   #获取行数
                self.label_2.setText("有"+str(input_table_rows)+"条结果")#标签
                self.compare=int(input_table_rows)
                input_table_colunms = input_table.shape[1]   #获取列数
                input_table_header = input_table.columns.values.tolist()   #获取头部目录
    
                self.tableWidget.setColumnCount(input_table_colunms)
                self.tableWidget.setRowCount(input_table_rows)
                self.tableWidget.setHorizontalHeaderLabels(input_table_header)
    
    
                for i in range(input_table_rows):
                    input_table_rows_values = input_table.iloc[[i]]
                    input_table_rows_values_array = np.array(input_table_rows_values)
                    input_table_rows_values_list = input_table_rows_values_array.tolist()[0]
                    for j in range(input_table_colunms):
                        input_table_items_list = input_table_rows_values_list[j]
                        input_table_items = str(input_table_items_list)
                        newItem = QTableWidgetItem(input_table_items)
                        newItem.setTextAlignment(Qt.AlignHCenter|Qt.AlignVCenter)
                        self.tableWidget.setItem(i, j, newItem)
    #修饰表格
                self.tableWidget.verticalHeader().setVisible(False)
    
                M =0
                N =0
                for M in range(input_table_rows):
                    for N in range(input_table_colunms):
                        if 'nan' == self.tableWidget.item(M,N).text():
                            self.tableWidget.setItem(M,N,QTableWidgetItem(0))
                        else:
                            self.tableWidget.setItem(M,N,QTableWidgetItem(str(self.tableWidget.item(M,N).text())))
            else:
                self.centralWidget.show()
    
    #====================对table表中的内容修改====================
        def table_insert(self):
            row = self.tableWidget.rowCount()
            self.tableWidget.insertRow(row)
            item_id = QTableWidgetItem("1")
            item_id.setFlags(Qt.ItemIsSelectable | Qt.ItemIsEnabled)  # 设置物件的状态为只可被选择（未设置可编辑）
            item_name = QTableWidgetItem("door") #我们要求它可以修改，所以使用默认的状态即可
            item_pos = QTableWidgetItem("(1,2)")
            item_pos.setFlags(Qt.ItemIsSelectable | Qt.ItemIsEnabled)  # 设置物件的状态为只可被选择
            self.tableWidget.setItem(row, 0, item_id)
            self.tableWidget.setItem(row, 1, item_name)
            self.tableWidget.setItem(row, 2, item_pos)
    
        def table_update(self):
            row_select = self.tableWidget.selectedItems()
            if len(row_select) == 0:
                return
            id = row_select[0].text()
            new_name = row_select[1].text()
    
        def table_delete(self):
            row_select = self.tableWidget.selectedItems()
            if len(row_select) == 0:
                return
            id = row_select[0].text()
            row = row_select[0].row()
            self.table.removeRow(row)
    
    #===============导出Table表中的数据。并保存在Excel中======================
        def save_table(self):
            rows = self.tableWidget.rowCount()
            columns=self.tableWidget.columnCount()
            if rows == self.compare:
                student_all_message=[]
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        student_all_message.append(self.tableWidget.item(rows_index,columns_index).text())
    
                rows_index=0
                columns_index=0
                wb = load_workbook(path_openfile_name)
                ws = wb.active
                m=0
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        ws.cell(row = rows_index+2, column = columns_index+1).value = student_all_message[m]
                        m+=1
                wb.save(path_openfile_name)
            else:
                wb = load_workbook(path_openfile_name)
                ws = wb.active
                I = 0
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        try:
                            key = self.use_key[I]
                            ws.cell(row=key, column=columns_index+1).value = self.tableWidget.item(rows_index,columns_index).text()
                        except:pass
                        try:
                            key_0=self.use_key_0[I]
                            ws.cell(row=key_0, column=columns_index+1).value = self.tableWidget.item(rows_index,columns_index).text()
                        except:pass
                        try:
                            key_1 = self.use_nogrates_key[I]
                            ws.cell(row=key_1, column=columns_index+1).value = self.tableWidget.item(rows_index,columns_index).text()
                        except:pass
                    I += 2
                wb.save(path_openfile_name)
    
    #===============按学号检索====================
        def number_find(self):
            rows = self.tableWidget.rowCount()
            columns=self.tableWidget.columnCount()
            self.key_number=self.finish_number
            key_number_find =[]
            wb = load_workbook(path_openfile_name)
            ws = wb.active
            try:
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        sheet_number = ws.cell(row = rows_index+2, column = columns_index+1).value
                        if self.key_number == sheet_number:
                           key_number_find.append(rows_index+2)
                           key_number_find.append(columns_index+1)
                        else:
                            pass
            except : pass
    #收集对应学号在excel中的位置
    
            input_table = pd.read_excel(path_openfile_name)
            input_table_header = input_table.columns.values.tolist()   #获取头部目录
            self.tableWidget.setColumnCount(columns)
            length=int(len(key_number_find)/2)
            self.label_2.setText("有"+str(length)+"条结果")#标签
            self.tableWidget.setRowCount(length)
            self.tableWidget.setHorizontalHeaderLabels(input_table_header)
            I = 0
            length_0 = length*2
            while I <length_0:
                length_1 = length_0 -I
                Q = 2
                while Q < length_1:
                    if key_number_find[I] == key_number_find[Q+I]:
                        key_number_find[Q+I] = 'NO'
                        key_number_find[Q+I+1] = 'NO'
                        Q+=2
                    else: Q+=2
                I+=2
    
            while 'NO' in key_number_find:
                key_number_find.remove('NO')
    #提炼出位置
            I = 0
            M = 0
            Q = len(key_number_find)
            while I< (int(Q)):
                N = 0
                for columns_index_0 in range (columns):
                    new_items= ws.cell(row = key_number_find[I], column = columns_index_0+1).value
                    self.tableWidget.setItem(M,N,QTableWidgetItem(str(new_items)))
                    N+=1
                I+=2
                M+=1
    
            self.use_key = []
            self.use_key = key_number_find
    
    #==============按老师检索===================
        def name_find(self):
            rows =self.tableWidget.rowCount()
            columns =self.tableWidget.columnCount()
            self.key_name1 =self.teacher_name
            self.key_name2 =self.test_name
            key_name1_find =[]
            key_name2_find =[]
            key_name_find =[]
            wb = load_workbook(path_openfile_name)
            ws = wb.active
            try:
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        sheet_name1 = ws.cell(row = rows_index+2, column = columns_index+1).value
                        if self.key_name1 == sheet_name1:
                            key_name1_find.append(rows_index+2)
                            key_name1_find.append(columns_index+1)
                        else:
                            pass
            except : pass
    #收集老师名字在excek中的位置
            try:
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        sheet_name2 = ws.cell(row = rows_index+2, column = columns_index+1).value
                        if self.key_name2 == sheet_name2:
                            key_name2_find.append(rows_index+2)
                            key_name2_find.append(columns_index+1)
                        else:
                            pass
            except : pass
    #收集对应实验在excel中的位置
            I = 0
            if int(len(key_name1_find))>= int(len(key_name2_find)):
                Q = int(len(key_name1_find))
            else:
                Q = int(len(key_name2_find))
            while I < Q:
                P = 2
                while P < Q -I:
                    if key_name1_find[I] == key_name2_find[I+P]:
                        key_name_find.append(key_name1_find[I])
                        key_name_find.append(key_name1_find[I+1])
                    P+=2
                I+=2
    
            input_table = pd.read_excel(path_openfile_name)
            input_table_header = input_table.columns.values.tolist()   #获取头部目录
            self.tableWidget.setColumnCount(columns)
            length=int(len(key_name_find)/2)
            self.label_2.setText("有"+str(length)+"条结果")#标签
            self.tableWidget.setRowCount(length)
            self.tableWidget.setHorizontalHeaderLabels(input_table_header)
    
            I = 0
            M = 0
            Q = len(key_name_find)
            while I< (int(Q)):
                N = 0
                for columns_index_0 in range (columns):
                    new_items= ws.cell(row = key_name_find[I], column = columns_index_0+1).value
                    self.tableWidget.setItem(M,N,QTableWidgetItem(new_items))
                    N+=1
                I+=2
                M+=1
    
            self.use_key_0 = []
            self.use_key_0 = key_name_find
    
     #===============获取需要检索的学号和教师名字=============
        def text_changed(self,text):
            number=[]
            number.append(self.lineEdit.text())
            self.finish_number=number[-1]
    
        def selectionchange(self):
            self.teacher_name=self.comboBox.currentText()
        def selectionchange_0(self):
            self.test_name=self.comboBox_2.currentText()
    
    #====================显示无成绩人员===================
        def no_grates(self):
            rows = self.tableWidget.rowCount()
            columns=self.tableWidget.columnCount()
            key_nogrates_find =[]
            wb = load_workbook(path_openfile_name)
            ws = wb.active
            try:
                for rows_index in range(rows):
                    for columns_index in range (columns):
                        sheet_number = ws.cell(row = rows_index+2, column = columns_index+1).value
                        if '' == sheet_number or '0'== sheet_number:
                            key_nogrates_find.append(rows_index+2)
                            key_nogrates_find.append(columns_index+1)
                        else:
                            pass
            except : pass
    #收集没有成绩的在excel中的位置
    
            length=int(len(key_nogrates_find)/2)
            I = 0
            length_0 = length*2
            while I <length_0:
                length_1 = length_0 -I
                Q = 2
                while Q < length_1:
                    if key_nogrates_find[I] == key_nogrates_find[Q+I]:
                        key_nogrates_find[Q+I] = 'NO'
                        key_nogrates_find[Q+I+1] = 'NO'
                        Q+=2
                    else: Q+=2
                I+=2
    
            while 'NO' in key_nogrates_find:
                key_nogrates_find.remove('NO')
    #提炼出位置
            length=int(len(key_nogrates_find)/2)
            input_table = pd.read_excel(path_openfile_name)
            input_table_header = input_table.columns.values.tolist()   #获取头部目录
            self.tableWidget.setColumnCount(columns)
            self.tableWidget.setRowCount(length)
            self.label_2.setText("有"+str(length)+"条结果")#标签
            self.tableWidget.setHorizontalHeaderLabels(input_table_header)
            I = 0
            M = 0
            Q = len(key_nogrates_find)
            while I< (int(Q)):
                N = 0
                for columns_index_0 in range (columns):
                    new_items= ws.cell(row = key_nogrates_find[I], column = columns_index_0+1).value
                    self.tableWidget.setItem(M,N,QTableWidgetItem(new_items))
                    N+=1
                I+=2
                M+=1
    
            self.use_nogrates_key = []
            self.use_nogrates_key = key_nogrates_find
    
    #=============显示界面=================
    if __name__=="__main__":
        import sys
    
        app=QtWidgets.QApplication(sys.argv)
        myshow=mywindow()
        myshow.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
