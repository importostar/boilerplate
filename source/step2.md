---
title: step2
date: 2020-05-07
---
Example Python program step2.py

## Modules

* from tkinter import *
* import tkinter as tk
* import tkinter.ttk as ttk
* import datetime

## Classes

* class Use_Frame(tk.Frame):
* class Use_Label(tk.Label):
* class Use_Entry(tk.Entry):
* class Use_Radio(tk.Radiobutton):

## Methods

* def __init__(self, master=None):
* def __init__(self, master=None):
* def __init__(self, master=None):
* def __init__(self, master=None):

## Code

Python tkinter example

    from tkinter import *
    import tkinter as tk
    import tkinter.ttk as ttk
    import datetime
    
    ##############################################################################
    #フレーム
    class Use_Frame(tk.Frame):
        def __init__(self, master=None):
            tk.Frame.__init__(self, master)
    ##############################################################################
    #ラベル
    class Use_Label(tk.Label):
        def __init__(self, master=None):
            tk.Label.__init__(self, master)
    ###############################################################################
    #エントリー
    class Use_Entry(tk.Entry):
        def __init__(self, master=None):
            tk.Entry.__init__(self, master)
    ##############################################################################
    #ラジオボタン(step2.pyで追加)
    class Use_Radio(tk.Radiobutton):
        def __init__(self, master=None):
            tk.Radiobutton.__init__(self, master)
    ##############################################################################
    
    root = tk.Tk()
    root.title("家計簿")
    
    #****************************************************************************#
    #日付の取得
    day = datetime.datetime.now()
    day = day.strftime("%Y/%m/%d")
    
    #****************************************************************************#
    #Frame_date(日付の入力)
    #ラベル、エントリーの作成
    Frame_date = Use_Frame(root)
    Frame_date.grid(column=0, row=0)
    
    Label_date_1 = Use_Label(Frame_date)
    Label_date_1.grid(column=0, row=0)
    Label_date_1["text"] = "日付の入力"
    
    Entry_date = Use_Entry(Frame_date)
    Entry_date.grid(column=1, row=0)
    Entry_date.insert(0, day)
    #****************************************************************************#
    #Frame_item(品目の選択)(step2.pyで追加)
    #ラジオボタンの作成
    Frame_item = Use_Frame(root)
    Frame_item.grid(column=0, row=1)
    
    Label_radio = Use_Label(Frame_item)
    Label_radio.grid(column=0, row=0)
    Label_radio["text"] = "品目を選択"
    
    Dict_item = {"1": "娯楽費　", "2": "食費　　", "3": "交通費　", "4": "日用品費"}
    
    for i in range(len(Dict_item)):
        Radio = Use_Radio(Frame_item)
        Radio.grid(column=0, row=i + 1)
        Radio["text"] = Dict_item[str(i + 1)]
    #****************************************************************************#
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
