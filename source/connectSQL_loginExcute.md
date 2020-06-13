---
title: connectSQL_loginExcute
date: 2020-05-07
---
Example Python program connectSQL_loginExcute.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from pymssql import connect
* from loginDisplay import *
* from mainWindow import *
* from PyQt5.QtWidgets import QApplication, QMainWindow, QTextBrowser, QDialog, QTableWidget, QTableWidgetItem
* from PyQt5.QtCore import QDateTime, Qt

## Classes

* class login(QDialog):
* class mainW(QMainWindow):

## Methods

* def __init__(self):
* def clicked_regit(self):
* def clicked_mainWindow(self):
* def __init__(self):
* def clicked_inputButton(self):
* def clicked_outputButton(self):
* def clicked_search_Button(self):
* def clicked_changeButton(self):
* def clieked_showToolButton(self):

## Code

Example Python PyQt program :

    import sys
    from pymssql import connect
    from loginDisplay import *
    from mainWindow import *
    from PyQt5.QtWidgets import QApplication, QMainWindow, QTextBrowser, QDialog, QTableWidget, QTableWidgetItem
    from PyQt5.QtCore import QDateTime, Qt
    
    
    class login(QDialog):
        def __init__(self):
            QDialog.__init__(self)
            self.loginUI = Ui_Dialog()
            self.loginUI.setupUi(self)
            # self.f = 0
    
        def clicked_regit(self):
            username = self.loginUI.user_lineEdit
            password = self.loginUI.passwd_lineEdit
    
            uName = username.text()
            uPassword = password.text()
    
            if len(uName) >= 10 or 12 < len(uPassword) or len(uPassword) < 6:
                text = "密码长度6-16位 | 用户名长度为10位以内！！！"
                self.loginUI.showsth_textBrowser.setText(text)
    
            # 连接数据库
            try:
                conn0 = connect(
                    host='localhost',
                    port='1433',
                    database='WareHouse',
                    charset='utf8')
                if conn0:
                    print("连接成功")
                cursor0 = conn0.cursor()
    
                # 判断用户是否存在
                print(uName)
                sql = 'select * from userinfo where username=%s'
                cursor0.execute(sql, uName)
                result = cursor0.fetchall()
                if result:
                    text = '用户名已经存在，请重新注册！！！'
                    self.loginUI.showsth_textBrowser.setText(text)
                else:
                    sql = 'insert into userinfo(username, userpasswd)values(%s, %s)'
                    result = cursor0.execute(sql, (uName, uPassword))
                    print(result)
                    conn0.commit()
    
                    text = '注册成功'
                    self.loginUI.showsth_textBrowser.setText(text)
            except Exception as e:
                text = '未知错误' + e
                print('未知错误' + e)
                self.loginUI.showsth_textBrowser.setText(text)
            finally:
                cursor0.close()
                conn0.close()
    
        def clicked_mainWindow(self):
            # 关闭登录界面
            global cursor, conn
            username = self.loginUI.user_lineEdit
            password = self.loginUI.passwd_lineEdit
    
            uName = username.text()
            uPassword = password.text()
    
            try:
                conn = connect(
                    server='DESKTOP-CEP3TV3',
                    user='sa',
                    password='lumia030395',
                    database='WareHouse')
                if conn:
                    print("连接成功")
                cursor = conn.cursor()
    
                sql = 'select * from userinfo where username=%s and userpasswd=%s'
                cursor.execute(sql, (uName, uPassword))
                result = cursor.fetchall()
                conn.commit()
                if result:
                    # self.f = 1
                    print('登录成功')
                    self.close()
                else:
                    text = '登录失败，用户名或密码错误！'
                    self.loginUI.showsth_textBrowser.setText(text)
            except Exception as e:
                print(e)
                text = '警告，不合规范的输入：' + str(e)
                self.mainUI.INOUT_Display.setText(text)
            finally:
                cursor.close()
                conn.close()
    
    
    class mainW(QMainWindow):
        def __init__(self):
            QMainWindow.__init__(self)
            self.mainUI = Ui_MainWindow()
            self.mainUI.setupUi(self)
            self.pNo = 1
    
        # 入库
        def clicked_inputButton(self):
            global cursor1, conn
            pName = self.mainUI.name_lineEdit.text()
            pNum = self.mainUI.number_lineEdit.text()
            # 单价，逻辑有改动
            pPrice = self.mainUI.no_lineEdit.text()
            pDateIN = QDateTime.currentDateTime().toString(Qt.ISODate)
    
            # test
            print(pName, pNum, pPrice, pDateIN)
    
            try:
                conn = connect(
                    host='localhost',
                    port='1433',
                    database='WareHouse',
                    charset='utf8')
                if conn:
                    print("连接成功")
                cursor1 = conn.cursor()
    
                sql1 = 'select * from warehouse where pdname=%s '
                cursor1.execute(sql1, pName)
                result = cursor1.fetchall()
                conn.commit()
                print(result)
                if not result:
                    text = '新存入产品' + pName + ',已入库'
                    self.mainUI.INOUT_Display.setText(text)
                    sqlUpdate = 'insert into warehouse(pdname, pdno, pdnumber, pdprice) values (%s, %d, %d, %d)'
                    cursor1.execute(sqlUpdate, (pName, self.pNo, pNum, pPrice))
                    conn.commit()
                    # 操作记录
                    sqlPROC = 'EXEC changingInfo  @pdname=%s, @pdnumber=%d, @pddateIN=%s, @pdprice=%d, @pdno=%d, @changingType=%s'
                    cursor1.execute(sqlPROC, (pName, pNum, pDateIN, pPrice, self.pNo, '入库'))
                    conn.commit()
                    self.pNo += 1
                elif result[0][0] == pName:
                    text = '产品' + pName + '库存已增加'
                    self.mainUI.INOUT_Display.setText(text)
                    sqlUpdate = 'Update warehouse Set pdnumber=pdnumber+%d where pdname=%s'
                    cursor1.execute(sqlUpdate, (pNum, pName))
                    conn.commit()
                    # 操作记录
                    sqlPROC = 'EXEC changingInfo  @pdname=%s, @pdnumber=%d, @pddateIN=%s, @pdprice=%d, @pdno=%d, @changingType=%s'
                    cursor1.execute(sqlPROC, (pName, pNum, pDateIN, pPrice, str(result[0][2]), '库存更新'))
                    conn.commit()
    
            except Exception as e:
                print(e)
                text = '警告，不合规范的输入：' + str(e)
                self.mainUI.INOUT_Display.setText(text)
            finally:
                cursor1.close()
                conn.close()
    
        # 出库
        def clicked_outputButton(self):
            global cursor, conn
            pName = self.mainUI.name_lineEdit.text()
            pNum = self.mainUI.number_lineEdit.text()
            pDateIN = QDateTime.currentDateTime().toString(Qt.ISODate)
            pPrice = self.mainUI.no_lineEdit.text()
    
            try:
                conn = connect(
                    host='localhost',
                    port='1433',
                    database='WareHouse',
                    charset='utf8')
                if conn:
                    print("连接成功")
                cursor = conn.cursor()
    
                sql1 = 'select * from warehouse where pdname=%s '
                cursor.execute(sql1, pName)
                result = cursor.fetchall()
                conn.commit()
    
                print(result)
                # 是否存在pName产品
                if not result:
                    text = '仓库中没有此产品'
                    self.mainUI.INOUT_Display.setText(text)
                elif result[0][0] == pName:
                    # 出库数目判断
                    Num = int(result[0][2]) - int(pNum)
                    print(Num)
                    if Num < 0:
                        text = '出库失败，库存数目不足！目前数目：' + str(result[0][2])
                        self.mainUI.INOUT_Display.setText(text)
                    elif int(result[0][3]) != int(pPrice):
                        text = '出库失败，库存单价不一致！目前单价：' + str(result[0][3])+ '元'
                        self.mainUI.INOUT_Display.setText(text)
                    elif Num >= 0:
                        # 出库操作
                        sqlUpDate = 'Update warehouse Set pdnumber=pdnumber-%d where pdname=%s'
                        cursor.execute(sqlUpDate, (pNum, pName))
                        conn.commit()
    
                        # 操作记录
                        sqlPROC = 'EXEC changingInfo  @pdname=%s, @pdnumber=%d, @pddateIN=%s, @pdprice=%s,@pdno=%d, @changingType=%s'
                        cursor.execute(sqlPROC, (pName, pNum, pDateIN, result[0][3], self.pNo, '出库'))
                        conn.commit()
    
                        text = '出库成功,目前数目：' + str(Num)
                        self.mainUI.INOUT_Display.setText(text)
    
            except Exception as e:
                print(e)
                text = '警告，不合规范的输入：' + str(e)
                self.mainUI.INOUT_Display.setText(text)
            finally:
                cursor.close()
                conn.close()
    
        # 查询产品库存信息
        def clicked_search_Button(self):
            global cursor, conn
            wantToFind = self.mainUI.search_lineEdit.text()
    
            try:
                conn = connect(
                    host='localhost',
                    port='1433',
                    database='WareHouse',
                    charset='utf8')
                if conn:
                    print("连接成功")
                cursor = conn.cursor()
                parameter = '%' + wantToFind + '%'
                print(parameter)
                sqlWantToFind = 'select * from warehouse where pdname like %s'
                cursor.execute(sqlWantToFind, parameter)
                result = cursor.fetchall()
                conn.commit()
                print(result)
                if result:
                    # 初始化显示界面
                    self.mainUI.searchView.setRowCount(len(result))
                    self.mainUI.searchView.setColumnCount(4)
                    self.mainUI.searchView.setHorizontalHeaderLabels(['产品名', '编号', '库存数目', '单价（元）'])
                    for i in range(len(result)):
                        for j in range(4):
                            newItem = QTableWidgetItem(str(result[i][j]))
                            self.mainUI.searchView.setItem(i, j, newItem)
                else:
                    self.mainUI.searchView.setRowCount(1)
                    self.mainUI.searchView.setColumnCount(1)
                    newItem = QTableWidgetItem('没有查询到相关库存信息')
                    self.mainUI.searchView.setItem(0, 0, newItem)
            except Exception as e:
                print(e)
                text = '警告，不合规范的输入：' + str(e)
                self.mainUI.INOUT_Display.setText(text)
            finally:
                cursor.close()
                conn.close()
    
        # 库存产品信息维护
        def clicked_changeButton(self):
            global cursor, conn
            No = self.mainUI.lineEdit_no.text()
            Name = self.mainUI.lineEdit_name.text()
            Price = self.mainUI.lineEdit_price.text()
            pDateIN = QDateTime.currentDateTime().toString(Qt.ISODate)
    
            try:
                conn = connect(
                    host='localhost',
                    port='1433',
                    database='WareHouse',
                    charset='utf8')
                if conn:
                    print("连接成功")
                cursor = conn.cursor()
                sql0 = 'select pdno from warehouse where pdno=%d'
                cursor.execute(sql0, No)
                result = cursor.fetchall()
                print(result)
                # 判断需要维护的产品是否存在
                if result:
                    if not Name:
                        sqlChange = 'Update warehouse set pdprice=%d where pdno=%d'
                        cursor.execute(sqlChange, (Price, No))
    
                    elif not Price:
                        sqlChange = 'Update warehouse set pdname=%s where pdno=%d'
                        cursor.execute(sqlChange, (Name, No))
                    else:
                        sqlChange = 'Update warehouse set pdname=%s, pdprice=%d where pdno=%d'
                        cursor.execute(sqlChange, (Name, Price, No))
                    conn.commit()
    
                    sqlWantToFind = 'select * from warehouse where pdno=%d'
                    cursor.execute(sqlWantToFind, No)
                    result1 = cursor.fetchall()
                    conn.commit()
    
                    # 操作记录
                    sqlPROC = 'EXEC changingInfo  @pdname=%s, @pdnumber=%d, @pddateIN=%s, @pdprice=%s, @pdno=%d, @changingType=%s'
                    cursor.execute(sqlPROC, (Name, No, pDateIN, Price, '信息维护结果'))
                    conn.commit()
    
                    print(result1)
                    self.mainUI.changeView.setColumnCount(4)
                    self.mainUI.changeView.setRowCount(1)
                    self.mainUI.changeView.setHorizontalHeaderLabels(['(新)产品名', '编号', '库存数目', '单价（元）'])
                    for j in range(4):
                        newItem1 = QTableWidgetItem(str(result1[0][j]))
                        self.mainUI.changeView.setItem(0, j, newItem1)
                else:
                    self.mainUI.changeView.setRowCount(1)
                    self.mainUI.changeView.setColumnCount(1)
                    newItem = QTableWidgetItem('维护失败，没有查询到相关库存信息')
                    self.mainUI.changeView.setItem(0, 0, newItem)
    
            except Exception as e:
                print(e)
                text = '警告，不合规范的输入：' + str(e)
                self.mainUI.INOUT_Display.setText(text)
            finally:
                cursor.close()
                conn.close()
    
        # 查询操作记录
        def clieked_showToolButton(self):
            try:
                conn = connect(
                    host='localhost',
                    port='1433',
                    database='WareHouse',
                    charset='utf8')
                if conn:
                    print("连接成功")
                cursor = conn.cursor()
    
                sql = 'select TOP 10 * from productINOUT'
                cursor.execute(sql)
                result = cursor.fetchall()
                conn.commit()
    
                print(result)
                if result:
                    # 初始化显示界面
                    self.mainUI.changed_TableView.setRowCount(len(result))
                    self.mainUI.changed_TableView.setColumnCount(6)
                    self.mainUI.changed_TableView.setHorizontalHeaderLabels(['时间', '操作说明', '产品名', '编号', '数目', '单价'])
                    for i in range(len(result)):
                        for j in range(6):
                            newItem = QTableWidgetItem(str(result[i][j]))
                            self.mainUI.changed_TableView.setItem(i, j, newItem)
                else:
                    self.mainUI.changed_TableView.setRowCount(1)
                    self.mainUI.changed_TableView.setColumnCount(1)
                    newItem = QTableWidgetItem('没有查询到任何操作信息')
                    self.mainUI.changed_TableView.setItem(0, 0, newItem)
    
            except Exception as e:
                print(e)
                text = '警告，不合规范的输入：' + str(e)
                self.mainUI.INOUT_Display.setText(text)
            finally:
                cursor.close()
                conn.close()
    
    
    if __name__ == '__main__':
        # 每一个PyQt5程序必须创建一个application对象，
        app = QApplication(sys.argv)  # sys.argv是命令行参数，可以通过命令启动的时候传递参数。
        # 生成实例（对象）
        mainDisplay = mainW()
        loginDisplay = login()
        # 主界面显示
        mainDisplay.show()
        # # 点击"请登录按钮" 弹出-登录注册-窗口
        mainDisplay.mainUI.loginClicked.clicked.connect(loginDisplay.show)
        # 用户注册，将账号密码保存到数据库中
        loginDisplay.loginUI.login_Button.clicked.connect(loginDisplay.clicked_regit)
        # 用户登录
        loginDisplay.loginUI.login_Button.clicked.connect(loginDisplay.clicked_mainWindow)
        # 入库
        mainDisplay.mainUI.input_Button.clicked.connect(mainDisplay.clicked_inputButton)
        # 出库
        mainDisplay.mainUI.output_Button.clicked.connect(mainDisplay.clicked_outputButton)
        # 查询
        mainDisplay.mainUI.search_Button.clicked.connect(mainDisplay.clicked_search_Button)
        # 保存修改
        mainDisplay.mainUI.pushButton_3.clicked.connect(mainDisplay.clicked_changeButton)
    
        # 查询操作记录
        mainDisplay.mainUI.toolButton.clicked.connect(mainDisplay.clieked_showToolButton)
        # 退出程序
        sys.exit(app.exec_())  # exec_()方法的作用是“进入程序的主循环直到exit()被调用”
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
