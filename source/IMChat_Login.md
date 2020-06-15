---
title: IMChat_Login
date: 2020-05-07
---
Example Python program IMChat_Login.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* #import tkinter as tk 导入python自带的gui tkinter 这样需要前面加包名调用，或者定义别名
* from tkinter import * #这样导入方法直接调用即可不需要用包调
* import ConnctionForMySqlDBC as conn
* import tkinter.messagebox as alert

## Methods

* def loginBtnClick(userE,passwordE):
* def RegisterBtnClick():
* def FindPasswordBtnClick():
* def ConnectionJDBCForMySQL():
* def Init_LoginFream():

## Code

Python tkinter example

    # encoding=utf8
    #import tkinter as tk 导入python自带的gui tkinter 这样需要前面加包名调用，或者定义别名
    from tkinter import * #这样导入方法直接调用即可不需要用包调
    import ConnctionForMySqlDBC as conn
    import tkinter.messagebox as alert
    
    #方法区域
    #登陆按钮方法
    def loginBtnClick(userE,passwordE):
    
        #获取客户输入的user以及password
        user = userE.get()
        password = passwordE.get()
        print ('用户名：'+ user+'密码：'+ password)
        #连接数据库查询用户名以及密码
        #拼接查询的sql语句
        sql = "select account,password from user_db where account='"+user+"'and password='"+password+"'"
        #返回的数据
        data = conn.ConnctionForMySQLJDBC.executeSQL(sql)
        if user == "" and password == "":
            alert.showerror("消息", "输入不能为空！")
            return
    
        #简单判断用户名以及密码输入是否错误
        if data != None:
            userJDBC = data[0]
            passwordJDBC = data[1]
            if user == userJDBC and password == passwordJDBC:
                print("登陆成功")
                #登陆成功进入到主界面
    
        else:
            alert.showerror("消息","密码或者用户名输入错误请重新输入！")
            return
    
    #注册事件
    def RegisterBtnClick():
        print ('点击了注册')
    
    
    #找回密码事件
    def FindPasswordBtnClick():
        print ('点击找回密码')
    
    
    
    #连接数据库的事件
    def ConnectionJDBCForMySQL():
        print ('连接数据库中')
    
    
    #初始化窗口
    def Init_LoginFream():
        root = Tk()
        root.title("MIChat聊天")
        root.resizable(0, 0)  # 禁止窗口拉伸，里面参数width，height（width = False，height=False 默认值等于True）
        # 主容器大小
        root.geometry('500x300')
        # 初始化lable标签
        titL = Label()
        userL = Label(root, text='Account:', font=('微软雅黑', 11), width=10)
        passwordL = Label(root, text='Password:', font=('微软雅黑', 11), width=10)
    
        # lable 位置设置
        titL.place(relx=0.4, rely=0.1)
        userL.place(x=80, y=100)
        passwordL.place(x=80, y=130)
    
        # 初始化文本输入框user And Password
        userE = Entry(root, width=25)
        passwordE = Entry(root, width=25)
        # 设置user And Password位置
        userE.place(x=180, y=100)
        passwordE.place(x=180, y=130)
        # 接受输入框的字符串
    
    
        # 按钮区域
        # 登陆按钮
        loginBtn = Button(root, text='login', width='20', bg='#0072E3', font=('微软雅黑', 12), command=lambda:loginBtnClick(userE,passwordE))#lambda 实现传值 传里面对象
        loginBtn.place(x=150, y=180)
    
        # 注册按钮
        registerBtn = Button(root, text='注册账号', fg='blue', font=('微软雅黑', 7), command=RegisterBtnClick)
        registerBtn.place(x=370, y=98)
    
        # 找回密码按钮
        findPasswordBtn = Button(root, text='找回密码', fg='blue', font=('微软雅黑', 7), command=FindPasswordBtnClick)
        findPasswordBtn.place(x=370, y=125)
        # 循环消息
        root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
