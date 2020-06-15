---
title: excel_sum_GUI
date: 2020-05-07
---
Example Python program excel_sum_GUI.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* import openpyxl
* import os
* import glob
* import tkinter.messagebox as messagebox
* import tkinter.filedialog

## Classes

* class TkDemo():

## Methods

* def __init__(self):
* def newfile(self):
* def openfile(self):
* def savefile(self):
* def description(self):
* def about(self):
* def visionrc(self):
* def visionsheet(self):
* def getname(self):
* def getfilename(self):
* def getrc(self):
* def getfile(self):
* def getactive(self):
* def getnumber(self):
* def getagree(self):
* def allsubmit(self):

## Code

Python tkinter example

    from tkinter import *
    import openpyxl
    import os
    import glob
    import tkinter.messagebox as messagebox
    import tkinter.filedialog
    
    class TkDemo():
        def __init__(self):
            master = Tk()
            master.title('TK学习')
            # 创建菜单栏 (Menu)
            menubar = Menu(master)
            master.config(menu=menubar)
            # 创建文件下拉菜单
            filemenu = Menu(menubar, tearoff=0)
            menubar.add_cascade(label="文件", menu=filemenu)
            filemenu.add_command(label="新建···", command=self.newfile)
            filemenu.add_command(label="打开···", command=self.openfile)
            filemenu.add_command(label="保存", command=self.savefile)
            filemenu.add_command(label="关闭填写", command=master.quit)
            # 创建编辑下拉菜单
            # 创建帮助下拉菜单
            helpmenu = Menu(menubar,tearoff=0)
            menubar.add_cascade(label='帮助', menu=helpmenu)
            helpmenu.add_command(label='操作说明', command=self.description)
            helpmenu.add_command(label='关于', command=self.about)
    
            textmenu = Menu(menubar,tearoff=0)
            menubar.add_cascade(label='<---请先阅读帮助栏中的说明!!!', menu=helpmenu)
    
            # 文字 (Label)
            title = Label(master, text='这可能是你见过的最low的程序了', font='15', bg='white', fg='red')
            title.pack()
    
            # 问题1放在frame1中 (Frame)
            frame1 = Frame(master)
            frame1.pack(fill=X)
            # 问题
            label1 = Label(frame1, text='1,请选择你要合并的文件')
            label1.grid(row=1, column=0)
            # 按钮  (Button)
            self.filearray = []
            getname = Button(frame1, text='选择', command=self.getfile)
            getname.grid(row=1, column=1)
    
            # frame4中
            frame4 = Frame(master)
            frame4.pack(fill=X)
            label4 = Label(frame4, text='2,请选择你想要合并的sheet：')
            label4.grid(row=1, column=0)
            #查看按钮
            visionsheet = Button(frame4,text = "查看",command = self.visionsheet)
            visionsheet.grid(row=1,column =2)
    
            #选择合并范围
            frame5 = Frame(master)
            frame5.pack(fill=X)
            label5 = Label(frame5,text='3,该sheet里有如下所示的行数和列数：')
            label5.grid(row=1,column=0)
            visionrcl = Button(frame5,text = "查看",command = self.visionrc)
            visionrcl.grid(row=1,column =2)
            label5_1 = Label(frame5,text = '请输入你要合并的起始行:')
            label5_1.grid(row=2,column = 0)
            self.begin_row = StringVar()
            begin_row = Entry(frame5, textvariable=self.begin_row)
            begin_row.grid(row=2, column=1)
            label5_2 = Label(frame5,text = '请输入你要合并的结束行:')
            label5_2.grid(row=3,column = 0)
            self.end_row = StringVar()
            end_row = Entry(frame5, textvariable=self.end_row)
            end_row.grid(row=3, column=1)
            label5_3 = Label(frame5,text = '请输入你要合并的起始列:')
            label5_3.grid(row=4,column = 0)
            self.begin_col = StringVar()
            begin_col = Entry(frame5, textvariable=self.begin_col)
            begin_col.grid(row=4, column=1)
            label5_4 = Label(frame5,text = '请输入你要合并的结束列:')
            label5_4.grid(row=5,column = 0)
            self.end_col = StringVar()
            end_col = Entry(frame5, textvariable=self.end_col)
            end_col.grid(row=5, column=1)
            # 按钮  (Button)
            getrc = Button(frame5, text='点击确认', command=self.getrc)
            getrc.grid(row=1, column=3)
    
            #保存文件
            frame8 = Frame(master)
            frame8.pack(fill = X)
            label8 = Label(frame8,text = '4,请输入你要保存的文件的名字')
            label8.grid(row=1,column = 0)
            self.filename = StringVar()
            filename = Entry(frame8,textvariable = self.filename)
            filename.grid(row=1,column = 1)
            #确定按钮
            getfilename = Button(frame8,text = '确认',command = self.getfilename)
            getfilename.grid(row =1,column = 2)
            # frame9
            frame9 = Frame(master)
            frame9.pack()
            submit = Button(frame9, text='运行', command=self.allsubmit)
            submit.grid(row = 2,column  =5)
            master.mainloop()
    
      # 属性
        # 文件栏
        def newfile(self):
            self.file = open(r'test.txt', 'w')
            self.file.close()
            messagebox.showinfo('新建文件','您已成功创建个人资料文档')   # 显示对话框
        def openfile(self):
            f = open(r'test.txt', 'r')
            try:
                f_read=f.read()
                #f_read_decode=f_read.decode('utf-8')
                print(f_read)
            finally:
                f.close()
        def savefile(self):
            messagebox.showwarning('保存文件', '抱歉还没开发出这个功能QAQ')    # 显示对话框
    
        # 帮助栏
        def description(self):
            messagebox.showinfo('Description', '1.选择文件\n2.选择合并范围\n3.点击运行出结果 ')   # 显示对话框
        def about(self):
            messagebox.showinfo('about', '本小bug是比比博用来学习tk的 \n ----1.0版')   # 显示对话框
    
        # 名字
        def visionrc(self):
            messagebox.showinfo('visionrc','该sheet总共有%d行%d列' %(self.excel[self.sheetname].max_row,self.excel[self.sheetname].max_column))
        def visionsheet(self):
            # 得到sheet列表
            sheet_v = tkinter.Toplevel()
            # 列表  (Listbox)
            self.head = self.filearray[0]
            self.excel = openpyxl.load_workbook(self.head)
            self.sheetarray = self.excel.sheetnames  # 得到文件里的所有sheet的名字
            self.listbox = Listbox(sheet_v)
            self.listbox.grid(row=1, column=1)
            for item in self.sheetarray:
                self.listbox.insert(END, item)
            #确定按钮
            getsheet = Button(sheet_v, text="确定", command=self.getactive)
            getsheet.grid(row=2, column=1)
            sheet_v.mainloop()
    
        def getname(self):
            name = self.name.get()
            print(name)
        def getfilename(self):
            filename = self.filename.get()
        def getrc(self):
            self.min_row = self.begin_row.get()
            self.max_row = self.end_row.get()
            self.min_col = self.begin_col.get()
            self.max_col = self.end_col.get()
        def getfile(self):
            filenames = tkinter.filedialog.askopenfilenames()
            if len(filenames) != 0:
                string_filename = ""
                for i in range(0, len(filenames)):
                    self.filearray.append(str(filenames[i]))
                    string_filename += str(filenames[i]) + "\n"
        # sheet选择
        def getactive(self):
            self.sheetname = self.listbox.get(ACTIVE)
            print(self.listbox.get(ACTIVE))
    
        # 数字
        def getnumber(self):
            print(self.number.get())
    
        # 同意
        def getagree(self):
            print(self.agree.get())
    
        # 提交
        def allsubmit(self):
            test_row = 1
            test = openpyxl.load_workbook("test.xlsx")
            test.save(self.filename.get() + ".xlsx")
            for i in self.filearray:
                test = openpyxl.load_workbook(self.filename.get() +".xlsx")
                excel = openpyxl.load_workbook(i)
                sheetall = excel.sheetnames
                data = excel[self.sheetname]
                for row in data.iter_rows(self.min_row, self.max_row, self.min_col, self.max_col):
                    for i in row:  # row是一个tuple
                        print(i.value)
                    j = 0
                    for i in row:
                        j = j + 1
                        test["Sheet1"].cell(row=test_row, column=j).value = i.value
                    test_row = test_row + 1
                test.save(self.filename.get() +".xlsx")  # 文件打开的时候不能保存。
            messagebox.showinfo('Success', '恭喜您已成功合并 ')   # 显示对话框
    
    TkDemo()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
