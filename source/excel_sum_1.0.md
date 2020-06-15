---
title: excel_sum_1.0
date: 2020-05-07
---
Example Python program excel_sum_1.0.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import openpyxl
* import os
* import glob

## Code

Python example

    import openpyxl
    import os
    import glob
    
    filearray = []
    for filename in glob.glob(r"*.xlsx"):
        filearray.append(filename)
    # 以上是从pythonscripts文件夹下读取所有excel表格，并将所有的名字存储到列表filearray
    print("在默认文件夹下有%d个文档哦" % len(filearray))
    print(filearray)
    ge = len(filearray)
    head = filearray[0]
    excel = openpyxl.load_workbook(head)
    # test = openpyxl.load_workbook("test.xlsx")
    sheetall = excel.sheetnames #得到文件里的所有sheet的名字
    print("你要合并的文件里包含这些sheet：")
    for sh in range(0,len(sheetall)):
        print(sh , sheetall[sh])
    sheetnum = input("请选择你要合并的sheet序号：")
    data = excel[sheetall[int(sheetnum)]]#得到sheet对象
    print(data.max_row)
    print(data.max_column)
    max_col = data.max_column
    test_row = 1
    min_row = input("请输入你想要合并的起始行：")
    max_row = input("请输入你想要合并的结束行：")
    min_col = input("请输入你想要合并的起始列：")
    max_col = input("请输入你想要合并的结束行：")
    # for row in data.iter_rows(min_row = 1, max_row= 2,min_col= 1,max_col = 10):
    #     for i in row:#row是一个tuple
    #        print(i.value)
    #     j = 0
    #     for i in row:
    #         j = j +1
    #         test["Sheet1"].cell(row = test_row,column = j).value = i.value
    #     test_row = test_row+1
    # # test.save("test.xlsx")#文件打开的时候不能保存。
    for i in filearray:
        test = openpyxl.load_workbook("test.xlsx")
        excel = openpyxl.load_workbook(i)
        sheetall = excel.sheetnames
        data = excel[sheetall[int(sheetnum)]]
        for row in data.iter_rows(min_row, max_row, min_col, max_col):
            for i in row:  # row是一个tuple
                print(i.value)
            j = 0
            for i in row:
                j = j + 1
                test["Sheet1"].cell(row=test_row, column=j).value = i.value
            test_row = test_row + 1
        test.save("test.xlsx")  # 文件打开的时候不能保存。

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
