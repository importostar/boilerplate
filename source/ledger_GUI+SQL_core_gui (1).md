---
title: ledger_GUI+SQL_core_gui (1)
date: 2020-05-07
---
Example Python program ledger_GUI+SQL_core_gui (1).py

## Modules

* import tkinter as tk
* from core.sqlite import 完成的验收名单, session
* from datetime import date
* from db.data import data

## Classes

* class 录入界面基类(tk.Frame):
* class 多单选按钮框架(tk.LabelFrame):
* class 界面类(录入界面基类):

## Methods

* def __init__(self, master=None, **kw):
* def get_num_show(self, x):
* # def modified(self, event):
* def 写入数据(self):
* def __init__(self, master, msg, text=None, **kw):
* def __init__(self, conf, master=None, **kw):
* def 当前员工(self):
* def 当前工作(self):
* def 写入数据(self):

## Code

Python tkinter example

    import tkinter as tk
    
    BG = '#ececec'
    WIDTH = 50
    
    
    class 录入界面基类(tk.Frame):
        def __init__(self, master=None, **kw):
            tk.Frame.__init__(self, master=master, **kw)
            self.master.geometry('+480+50')
            self.master.configure(bg=BG)
            self.configure(bg=BG)
            self.pack(side=tk.LEFT)
            self.编号列表 = None
            tk.Label(self, text='单据详情', bg=BG, width=WIDTH).pack()
    
            self.text = tk.Text(self, width=62)
            self.text.pack()
    
            tk.Label(self,
                     text='在下面输入单据编号(可只输入流水号)',
                     bg=BG,
                     width=WIDTH
                     ).pack(anchor=tk.W)
            self.entry = tk.Entry(self)
            self.entry.pack(anchor=tk.W, fill=tk.BOTH)
            self.entry.insert(0, "DF2019-S")
            self.entry.focus_set()
    
            self.entry.bind('<Return>', self.get_num_show)  # 绑定回车键的功能
    
        def get_num_show(self, x):
            self.编号列表 = self.entry.get()  # todo:加个判断是否重复输入功能
            self.entry.delete(8, tk.END)
            self.text.insert(tk.END, self.编号列表)
            self.写入数据()
            self.text.insert(tk.END, '\n')
            self.text.see(tk.END)
    
            # 每次修改text以后，会自动调用这个，然后滚动到最后
            # def modified(self, event):
            #     self.txt.see(END)  # tkinter.END if you use namespaces
            # 还可以用这个绑定
            # self.txt.bind('<<Modified>>', self.modified)
            # 这个是原帖
            # http://stackoverflow.com/questions/17475116/
            # how-to-make-text-scroll-down-automatically
            # -whenever-text-overcomes-the-visual-ar
    
        def 写入数据(self):
            """向数据库写入数据"""
            raise NotImplementedError('必须重写此方法')
    
    
    class 多单选按钮框架(tk.LabelFrame):
        """自定义批量多选按钮"""
    
        def __init__(self, master, msg, text=None, **kw):
            """
            :param master: 宿主组件
            :param msg: pandas数据框
            :param text: 框架名称,字符串
            """
            tk.LabelFrame.__init__(self, master, text=text, relief=tk.RIDGE, **kw)
            self._当前值 = tk.StringVar()
            self._当前值.set(None)
            for id, row in msg.iterrows():
                tk.Radiobutton(self,
                               text=row['name'],
                               variable=self._当前值,
                               value=row['name'],
                               width=8,
                               justify=tk.LEFT,
                               pady=2,
                               bg=BG
                               ).pack(anchor=tk.W, padx=5)
            tk.Label(self, textvariable=self._当前值).pack()
    
    
    class 界面类(录入界面基类):
        def __init__(self, conf, master=None, **kw):
            录入界面基类.__init__(self, master, **kw)
            self.master.title('派 工')
            self.master.geometry('560x480+480+50')
            self.选择区 = tk.Frame(self.master, bg=BG)
            self.选择区.pack(side=tk.LEFT)
            self.员工 = 多单选按钮框架(self.选择区, conf[0], text='员工', pady=8, bg=BG)
            self.员工.pack(anchor=tk.W)
            self.工作 = 多单选按钮框架(self.选择区, conf[1], text='工作', pady=8, bg=BG)
            self.工作.pack(anchor=tk.W, pady=20)
    
        @property
        def 当前员工(self):
            return self.员工._当前值
    
        @property
        def 当前工作(self):
            return self.工作._当前值
    
        def 写入数据(self):
            from core.sqlite import 完成的验收名单, session
            from datetime import date
            session.add(完成的验收名单(P_ID=self.编号列表, date=date.today()))
            try:
                session.commit()
                self.text.insert(tk.END, '   记录成功!')
            except Exception:
                self.text.insert(tk.END,'    数据异常! 未保存!')
                session.rollback()
            session.close()
    
    
    if __name__ == '__main__':
        from db.data import data
    
        # 录入界面基类().mainloop()
        派工界面 = 界面类([data['员工信息'], data['工作类型']])
        派工界面.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
