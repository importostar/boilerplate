---
title: to_pdf
date: 2020-05-07
---
Example Python program to_pdf.py

## Modules

* import os
* import tkinter as tk
* from tkinter import ttk
* from tkinter import filedialog
* from tkinter import messagebox

## Classes

* class Application(tk.Tk):
* class MyMenu(object):

## Methods

* def init(self):
* def createWidgets(self):
* def __opendir(self):
* def __refresh(self, event=None):
* def addmenu(self, Menu):
* def __init__(self, root):
* def file_open(self):
* def file_new(self):
* def file_save(self):
* def edit_cut(self):
* def edit_copy(self):
* def edit_paste(self):
* def help_about(self):

## Code

Python tkinter example

    # coding:utf-8
    import os
    import tkinter as tk
    from tkinter import ttk
    from tkinter import filedialog
    from tkinter import messagebox
    
    
    class Application(tk.Tk):
        '''
        文件夹选择程序
            界面与逻辑分离
        '''
    
        def init(self):
            self.createWidgets()
    
        def createWidgets(self):
            '''界面'''
            self.title("网易歌词PDF生成工具V1.0")
            self.columnconfigure(0, minsize=50)
    
            # 定义一些变量
            self.keyvar = tk.StringVar()
            self.keyvar.set('选择类型')
            items = ['单曲', '歌单地址', '歌曲列表']
    
            # 先定义顶部和内容两个Frame，用来放置下面的部件
            topframe = tk.Frame(self, height=80)
            contentframe = tk.Frame(self)
            topframe.pack(side=tk.TOP)
            contentframe.pack(side=tk.TOP)
    
            # 顶部区域（四个部件）
            # -- 前三个直接用 tk 的 widgets，第四个下拉列表 tk 没有，ttk 才有，比较麻烦
            gcombobox = ttk.Combobox(topframe, values=items, textvariable=self.keyvar)
            gbutton = tk.Button(topframe, command=self.__opendir, text='生成PDF')
            # -- 绑定事件
            # gcombobox.bind('<ComboboxSelected>', func=self.__refresh) # 绑定 <ComboboxSelected> 事件
            # -- 放置位置
            gcombobox.grid(row=0, column=2)
            gbutton.grid(row=0, column=3)
    
            # 内容区域（三个部件）
            # -- 前两个滚动条一个竖直一个水平
            rightbar = tk.Scrollbar(contentframe, orient=tk.VERTICAL)
            bottombar = tk.Scrollbar(contentframe, orient=tk.HORIZONTAL)
            self.textbox = tk.Text(contentframe, yscrollcommand=rightbar.set, xscrollcommand=bottombar.set)
            # -- 放置位置
            rightbar.pack(side=tk.RIGHT, fill=tk.Y)
            bottombar.pack(side=tk.BOTTOM, fill=tk.X)
            self.textbox.pack(side=tk.LEFT, fill=tk.BOTH)
            # -- 设置命令
            rightbar.config(command=self.textbox.yview)
            bottombar.config(command=self.textbox.xview)
    
        def __opendir(self):
            '''打开文件夹的逻辑'''
            self.textbox.delete('1.0', tk.END)  # 先删除所有
    
            self.dirname = filedialog.askdirectory()  # 打开文件夹对话框
    
            if not self.dirname:
                messagebox.showwarning('警告', message='未选择文件夹！')  # 弹出消息提示框
    
            for eachdir in self.dirlist:
                self.textbox.insert(tk.END, eachdir + '\r\n')
    
            self.textbox.update()
    
        def __refresh(self, event=None):
            '''更新的逻辑'''
            self.textbox.delete('1.0', tk.END)  # 先删除所有
    
            for eachdir in self.dirlist:
                self.textbox.insert(tk.END, eachdir + '\r\n')
    
            self.textbox.update()
    
        def addmenu(self, Menu):
            '''添加菜单'''
            Menu(self)
    
    
    class MyMenu(object):
        '''菜单类'''
    
        def __init__(self, root):
            '''初始化菜单'''
            self.menubar = tk.Menu(root)  # 创建菜单栏
    
            # 创建“文件”下拉菜单
            filemenu = tk.Menu(self.menubar, tearoff=0)
            filemenu.add_command(label="打开", command=self.file_open)
            filemenu.add_command(label="新建", command=self.file_new)
            filemenu.add_command(label="保存", command=self.file_save)
            filemenu.add_separator()
            filemenu.add_command(label="退出", command=root.quit)
    
    
            # 创建“帮助”下拉菜单
            helpmenu = tk.Menu(self.menubar, tearoff=0)
            helpmenu.add_command(label="关于", command=self.help_about)
    
            # 将前面三个菜单加到菜单栏
            self.menubar.add_cascade(label="文件", menu=filemenu)
    
            self.menubar.add_cascade(label="帮助", menu=helpmenu)
    
            # 最后再将菜单栏整个加到窗口 root
            root.config(menu=self.menubar)
    
        def file_open(self):
            messagebox.showinfo('打开', '文件-打开！')  # 消息提示框
            pass
    
        def file_new(self):
            messagebox.showinfo('新建', '文件-新建！')  # 消息提示框
            pass
    
        def file_save(self):
            messagebox.showinfo('保存', '文件-保存！')  # 消息提示框
            pass
    
        def edit_cut(self):
            messagebox.showinfo('剪切', '编辑-剪切！')  # 消息提示框
            pass
    
        def edit_copy(self):
            messagebox.showinfo('复制', '编辑-复制！')  # 消息提示框
            pass
    
        def edit_paste(self):
            messagebox.showinfo('粘贴', '编辑-粘贴！')  # 消息提示框
            pass
    
        def help_about(self):
            messagebox.showinfo(title='关于：网易歌词PDF生成', message='作者：Tacey Wong \n verion 1.0 \n \n ',icon="info")  # 弹出消息提示框
    
    
    if __name__ == '__main__':
        # 实例化Application
        app = Application()
        app.init()
    
        # 添加菜单:
        app.addmenu(MyMenu)
    
        # 主消息循环:
        app.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
