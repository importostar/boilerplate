---
title: windowDemo1
date: 2020-05-07
---
Example Python program windowDemo1.py

## Modules

* import tkinter as tk
* from tkinter import *
* import pickle,os
* from tkinter.messagebox import *

## Methods

* def usr_login():
* def usr_sign_up():

## Code

Python tkinter example

    '''
    创建登陆窗口
    '''
    
    import tkinter as tk
    from tkinter import *
    import pickle,os
    from tkinter.messagebox import *
    
    
    window=tk.Tk()
    window.title("for windowDemo1")
    window.geometry('450x400')
    
    #定义画布
    canvas=tk.Canvas(window,height=200,width=500)
    image_file=tk.PhotoImage(file='D:/Program Files/1.gif')  #加载图片文件
    image=canvas.create_image(0,0,anchor='nw',image=image_file)
    canvas.pack(side='top')
    
    #user information
    tk.Label(window,text='User name:').place(x=50,y=150)
    tk.Label(window,text='Password:').place(x=50,y=190)
    
    var_usr_name=tk.StringVar() #定义变量
    var_usr_name.set('example@python.com')
    entry_usr_name=tk.Entry(window,textvariable=var_usr_name)
    entry_usr_name.place(x=160,y=150)
    
    var_usr_pwd=tk.StringVar()
    entry_usr_pwd=tk.Entry(window,textvariable=var_usr_pwd,show='*')
    entry_usr_pwd.place(x=160,y=190)
    
    
    def usr_login():
        # 获取用户名与密码
        usr_name = var_usr_name.get()
        usr_pwd = var_usr_pwd.get()
        try:
            abspath=os.path.abspath('.')
            data='test-absdcad'
            # path=r'c:\usrs\lenovo\deskop'
            filepath=os.path.join(abspath,'usrs_info.pickle')
            with open(filepath) as usrfile:
                usrinfo=pickle.load(usrfile)
        except FileNotFoundError:
            #若没有读取到usrfile，程序会创建这个文件，将admin的用户和密码写入。
            with open(filepath,'wb') as usrfile:
                usrinfp={'admin':'admin'}
                pickle.dump(usrinfo,usrfile)
    
        if usr_name in usrinfo:
            if usr_pwd==usrinfo[usr_name]:
                tk.messagebox.showinfo()
    def usr_sign_up():
        pass
    #login and sign up button
    btn_login=tk.Button(window,text='Login',command=usr_login)
    btn_login.place(x=160,y=230)
    
    btn_sign_up=tk.Button(window,text='Sign up',command=usr_sign_up)
    btn_sign_up.place(x=240,y=230)
    
    
    window.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
