---
title: rip_that_logfile
date: 2020-05-07
---
Example Python program rip_that_logfile.py

## Modules

* import re
* import tkinter
* import xlrd
* import xlwt
* from tkinter import simpledialog
* from tkinter import filedialog
* from openpyxl import workbook
* import openpyxl
* #Gets column number from the selected sheet for RID, Date and Time. Maybe the Order isn't important...
* #Appends all of the fieldIDs (this will be important for the layout of your main Import File). Removes the CF from the beginning

## Methods

* def findCell (excelBook, sheetNumber, row, columnNumber):
* def findColumnIndexNumber(stringToSearchFor, sheetNumber, excelBook):

## Code

Python tkinter example

    import re
    import tkinter
    import xlrd
    import xlwt
    from tkinter import simpledialog
    from tkinter import filedialog
    from openpyxl import workbook
    import openpyxl
    
    """
    This program essentially takes the logfile and given the RID, Date and Time from an Excel file (in that order)
    this will parse the logfile for data from that exact time and date and given a layout file from another page, will match them
    accordingly. The layout must have the field ID adjacent to the Field name.
    
    This file seems to be very difficult when working with times and dates, it must be Text (Excel seems to convert them to a number
    which makes it difficult to work with -- keep in mind that you need to return to a date in these instances).
    """
    
    def findCell (excelBook, sheetNumber, row, columnNumber):
        excelBook = excelBook
        sheet = excelBook.sheets()[sheetNumber]
        cell = sheet.cell(row, columnNumber)
        return cell
    
    def findColumnIndexNumber(stringToSearchFor, sheetNumber, excelBook):
        excelBook = excelBook
        mainSheet = excelBook.sheets()[sheetNumber]
        for mainSheet in excelBook.sheets():
            for rowidx in range(mainSheet.nrows):
                row = mainSheet.row(rowidx)
                for colidx, cell in enumerate(row):
                    if stringToSearchFor in cell.value:
                        return colidx
    
    root = tkinter.Tk()
    saveDirectory = filedialog.askdirectory()
    
    #Opens the workbook with openPyxl, only openPYXl can have over 300 columns -- necessary for larger tables/databases.
    xl_workbook = xlrd.open_workbook(filedialog.askopenfilename())
    
    insheet = xl_workbook.sheets()[0]
    sheet_two = xl_workbook.sheets()[1]
    
    #This file is the logfile.
    txtfile = open(r"C:\Users\Brian\Documents\Towns & Municipalities\Jackson County\WFREQINP.txt", encoding="utf8")
    #Reads the logfile into a single string, replaces all of the newlines as Python(or just my code) has difficulty working with newlines.
    lines = txtfile.read().replace('\n', '')
    
    openPy_workbook = openpyxl.Workbook()
    ws1 = openPy_workbook.active
    ws1.title = "SheetUno"
    
    #Gets column number from the selected sheet for RID, Date and Time. Maybe the Order isn't important...
    RID_column_index = findColumnIndexNumber("RID", 0, xl_workbook)
    date_column_index = findColumnIndexNumber("Date", 0, xl_workbook)
    time_column_index = findColumnIndexNumber("Time", 0, xl_workbook)
    
    #Array to hold RIDs, Dates, Times and FieldIDs & text for iteration later on.
    rids = []
    dates = []
    times = []
    fids = []
    text = []
    
    #Appends all RIDS, dates and times into the workbook.
    for row_idx in range(1, insheet.nrows):
        rids.append(int(findCell(xl_workbook, 0, row_idx, RID_column_index).value))
        dates.append(findCell(xl_workbook, 0, row_idx, date_column_index).value)
        times.append(findCell(xl_workbook, 0, row_idx, time_column_index).value)
    
    #Appends all of the appropriate data for the SPECIFIC dates and times. It will take NOTHING ELSE -- if your time is even a little bit off
    #this WILL fail!
    for x in range(len(dates)):
        text.append(re.findall("%s %s(.*?)]" % (dates[x],times[x]), lines))
        print ("%s %s" % (dates[x],times[x]))
    
    #Appends all of the fieldIDs (this will be important for the layout of your main Import File). Removes the CF from the beginning
    #of the fieldID since the logfile does not have the CF attached.
    for row_idx in range(1, sheet_two.nrows):
        fids.append(findCell(xl_workbook, 1, row_idx, 0).value.replace('CF', ''))
        ws1.cell(row=1, column=row_idx).value = findCell(xl_workbook, 1, row_idx, 1).value
    
    #Finds all text for each RID given their date via regex
    for x in range(len(text)):
        print (len(text[x]))
        if (len(text[x])==0):
            text[x] = re.findall("%s(.*?)]" % rids[x], lines)
            print (text[x])
            print (rids[x])
    
    #This will break down the text, then break it down again since the findall function turns the data into arrays, if you want a string
    #to work with, you'll need to get exact slice of the array you want, then in that slice, you'll find an array, you'll need the only/final
    #slice from that array and you'll have your information based on the fieldID.
    for fid in range(len(fids)):
        for x in range(len(text)):
            if (len(text[x])>1):
                truetext = text[x]
                fidder = fids[fid]
                truesttext = truetext[-1]
                listed = re.findall('%s": (.*?),' % fidder, truesttext)
                try:
                    ws1.cell(row=x+2, column=fid+1).value = listed[0]
                except:
                    pass
            else:
                truetext = text[x]
                fidder = fids[fid]
                truesttext = truetext[0]
                listed = re.findall('%s": (.*?),' % fidder, truesttext)
                try:
                    ws1.cell(row=x+2, column=fid+1).value = listed[0]
                except:
                    pass
    
    print (len(fids))
    print (fids)
    print (rids)
    print (dates)
    print (times)
    
    #Saves your workbook, my guy!
    openPy_workbook.save("%s\ripped.xlsx" % saveDirectory)
    
    print (len(text))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
