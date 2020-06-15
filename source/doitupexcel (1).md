---
title: doitupexcel (1)
date: 2020-05-07
---
Example Python program doitupexcel (1).py

## Modules

* import xlrd
* import xlwt
* import tkinter
* from tkinter import filedialog
* import editdistance
* import numpy

## Methods

* def findColumnIndexNumber(stringToSearchFor, sheetNumber, excelBook):
* def createArrayOfAddresses(indexNumber, sheetNumber, excelBook):
* def findString (excelBook, sheetNumber, iterator, columnNumber):
* def findCell (excelBook, sheetNumber, row, columnNumber):
* def updateAddressesAndAPNs():

## Code

Python tkinter example

    import xlrd
    import xlwt
    import tkinter
    from tkinter import filedialog
    import editdistance
    import numpy
    
    root = tkinter.Tk()
    allAPNAddresses = []
    allTableAddresses = []
    book = xlrd.open_workbook(filedialog.askopenfilename())
    copy_book = xlwt.Workbook()
    copy_sheet = copy_book.add_sheet("Initial")
    
    def findColumnIndexNumber(stringToSearchFor, sheetNumber, excelBook):
        excelBook = excelBook
        mainSheet = excelBook.sheets()[sheetNumber]
        for mainSheet in excelBook.sheets():
            for rowidx in range(mainSheet.nrows):
                row = mainSheet.row(rowidx)
                for colidx, cell in enumerate(row):
                    if cell.value == stringToSearchFor :
                        print (mainSheet.nrows)
                        print (mainSheet.name)
                        print (colidx)
                        print (rowidx)
                        return colidx
    
    def createArrayOfAddresses(indexNumber, sheetNumber, excelBook):
        excelBook = excelBook
        mainSheet = excelBook.sheets()[sheetNumber]
        data = []
        for i in range(1, mainSheet.nrows):
            cell = mainSheet.cell(i, indexNumber).value
            #print (cell)
            data.append(cell)
        return data
    
    def findString (excelBook, sheetNumber, iterator, columnNumber):
        excelBook = excelBook
        sheet = excelBook.sheets()[sheetNumber]
        cell = sheet.cell(iterator, columnNumber)
        whatIfound = cell.value
        return whatIfound
    
    def findCell (excelBook, sheetNumber, row, columnNumber):
        excelBook = excelBook
        sheet = excelBook.sheets()[sheetNumber]
        cell = sheet.cell(row, columnNumber)
        return cell
    
    #mainSheet.nrows
    
    allAPNAddresses = createArrayOfAddresses(findColumnIndexNumber("Property Address", 1, book), 1, book)
    #print (allAPNAddresses[0])
    #print (allAPNAddresses[2925])
    allTableAddresses = createArrayOfAddresses(findColumnIndexNumber("Table Address", 0, book), 0, book)
    addressMatchPercentage = []
    
    def updateAddressesAndAPNs():
    
    for m in range(0, 2926):
        addressMatchPercentage.append(0)
    print (len(addressMatchPercentage))
    addressMatchPercentage.append(0)
    
    
    tableAddressColumnNumber = findColumnIndexNumber("Table Address", 0, book)
    apnAddressColumnNumber = findColumnIndexNumber("Table APN", 0, book)
    for iterator in range(1, 5):
        print ("Running iteration #: %s" % iterator)
        addressText = findString(book, 0, iterator, tableAddressColumnNumber)
        #print (addressText)
        maxValue = addressMatchPercentage[0]
        arrayPosition = 0
    
    
    
    
        for addressIterator in range(0, 2926):
            s1 = addressText
            s2 = allAPNAddresses[addressIterator]
            levDistance = editdistance.eval(s1.lower(), s2.lower())
            ratio = (levDistance / max(len(s1), len(s2)))*100
            ratio = 100 - ratio
            #print (ratio)
            addressMatchPercentage[addressIterator] = ratio
            #print (addressMatchPercentage[addressIterator])
    
            for i in range(1,len(addressMatchPercentage)):
                if (addressMatchPercentage[i] > maxValue):
                    maxValue = addressMatchPercentage[i]
                    arrayPosition = i
    
        if maxValue >= 100:
            copy_sheet.write(iterator, tableAddressColumnNumber, allAPNAddresses[arrayPosition])
            copy_sheet.write(iterator, apnAddressColumnNumber, findString(book, 1, (arrayPosition + 1), apnAddressColumnNumber))
        elif maxValue >= 65:
            copy_sheet.write(iterator, tableAddressColumnNumber, allAPNAddresses[arrayPosition])
            copy_sheet.write(iterator, apnAddressColumnNumber, findString(book, 1, (arrayPosition + 1), apnAddressColumnNumber))
    print (len(addressMatchPercentage))
    
    copy_book.save("C:\Users\Brian\Documents\Python\good_enough.xls")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
