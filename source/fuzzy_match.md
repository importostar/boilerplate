---
title: fuzzy_match
date: 2020-05-07
---
Example Python program fuzzy_match.py

## Modules

* import xlrd
* import xlwt
* import tkinter
* from tkinter import filedialog
* from tkinter import simpledialog
* import editdistance
* import numpy
* from xlwt import Formula
* import openpyxl
* from openpyxl import load_workbook
* import time
* import untitled
* from openpyxl.workbook import Workbook
* from openpyxl.reader.excel import load_workbook, InvalidFileException
* import os
* import cProfile

## Methods

* def doesStringContainsAll(stringToParse, standardString):
* def findCell (excelBook, sheetNumber, row, columnNumber):
* def findString (excelBook, sheetNumber, iterator, columnNumber):
* def findColumnIndexNumber(stringToSearchFor, sheetNumber, excelBook):
* def createArrayForColumn(indexNumber, sheetNumber, excelBook):

## Code

Python tkinter example

    import xlrd
    import xlwt
    import tkinter
    from tkinter import filedialog
    from tkinter import simpledialog
    import editdistance
    import numpy
    from xlwt import Formula
    import openpyxl
    from openpyxl import load_workbook
    import time
    import untitled
    from openpyxl.workbook import Workbook
    from openpyxl.reader.excel import load_workbook, InvalidFileException
    import os
    import cProfile
    
    #Copy all of the data
    #Ask user the name of the Column which will be matched to page Sheet2
    #FindColumn, insert a column next to it
    #Perform Fuzzy String matching, then place best match into the appropriate row (per iteration), if none, enter #N/A
    #Save file
    
    
    def doesStringContainsAll(stringToParse, standardString):
        for c in stringToParse:
            if c not in standardString: return 0;
        return 1;
    
    def findCell (excelBook, sheetNumber, row, columnNumber):
        excelBook = excelBook
        sheet = excelBook.sheets()[sheetNumber]
        cell = sheet.cell(row, columnNumber)
        return cell
    
    def findString (excelBook, sheetNumber, iterator, columnNumber):
        excelBook = excelBook
        sheet = excelBook.sheets()[sheetNumber]
        cell = sheet.cell(iterator, columnNumber)
        whatIfound = cell.value
        return whatIfound
    
    def findColumnIndexNumber(stringToSearchFor, sheetNumber, excelBook):
        excelBook = excelBook
        mainSheet = excelBook.sheets()[sheetNumber]
        for mainSheet in excelBook.sheets():
            for rowidx in range(mainSheet.nrows):
                row = mainSheet.row(rowidx)
                for colidx, cell in enumerate(row):
                    if cell.value == stringToSearchFor :
                        return colidx
    
    def createArrayForColumn(indexNumber, sheetNumber, excelBook):
        excelBook = excelBook
        mainSheet = excelBook.sheets()[sheetNumber]
        data = []
        for i in range(1, mainSheet.nrows):
            cell = mainSheet.cell(i, indexNumber).value
            data.append(cell)
        return data
    
    root = tkinter.Tk()
    book = xlrd.open_workbook(filedialog.askopenfilename())
    saveDirectory = filedialog.askdirectory()
    
    copy_book = xlwt.Workbook()
    sheetOne = book.sheets()[0]
    sheetTwo = book.sheets()[1]
    copy_sheet = copy_book.add_sheet("Initial")
    
    address_from_system_column_index = findColumnIndexNumber("FADDRESS", 1, book)
    address_from_legacy_data_column_index = findColumnIndexNumber("Property Address", 0, book)
    allStandardizedDataArray = createArrayForColumn(address_from_system_column_index, 1, book)
    allSourceDataArray = createArrayForColumn(address_from_legacy_data_column_index, 0, book)
    
    addres_dict_short = [" ave"," st"," rd"," blvd"," ct"," ln"," dr"," pike"," ter"," terr"," 1st"," 2nd"," 3rd"," 4th"," 5th"," 6th"," 7th"," 8th"," 9th"," 10th"]
    address_dict_long = [" avenue"," street"," road"," boulevard"," court"," lane"," drive"," turnpike"," terrace"," terrace"," first"," second"," third"," fourth"," fifth"," sixth",
    " seventh"," eigth"," ninth"," tenth"]
    
    for iterator in range(1, sheetOne.nrows):
        print ("Running iteration #: %s" % iterator)
        text = findString(book, 0, iterator, address_from_legacy_data_column_index)
        print (text)
        matchPercentageArray = []
    
        for m in range(sheetTwo.nrows):
            matchPercentageArray.append(0)
        print (len(matchPercentageArray))
        #for levIterator in range(sheetTwo.nrows - 1):
        #    for i in range(len(matchPercentageArray)):
        #        matchPercentageArray[i] = 0
    
        maxValue = matchPercentageArray[0]
        arrayPosition = 0
    
    
    
    
    
        for levIterator in range(sheetTwo.nrows - 1):
            s1 = text
            s2 = allStandardizedDataArray[levIterator]
            levDistance = editdistance.eval(s1.lower(), s2.lower())
            ratio = (levDistance / max(len(s1), len(s2)))*100
            ratio = 100 - ratio
            matchPercentageArray[levIterator] = ratio
    
            for i in range(len(matchPercentageArray)):
                #print ("matchPercentageArray %s" % i)
                if (matchPercentageArray[i] > maxValue):
                    maxValue = matchPercentageArray[i]
                    arrayPosition = i
    
    
        if doesStringContainsAll(text.lower(), allStandardizedDataArray[arrayPosition].lower()) == 1:
            copy_sheet.write(iterator, 6, allStandardizedDataArray[arrayPosition])
    
        if doesStringContainsAll(allStandardizedDataArray[arrayPosition].lower(), text.lower()) == 1:
            copy_sheet.write(iterator, 7, allStandardizedDataArray[arrayPosition])
    
        for h in range(len(addres_dict_short)):
            if addres_dict_short[h] in text.lower():
                if doesStringContainsAll(text.lower().replace(addres_dict_short[h], address_dict_long[h]), allStandardizedDataArray[arrayPosition].lower()) == 1:
                    copy_sheet.write(iterator, 9, allStandardizedDataArray[arrayPosition])
    
            if address_dict_long[h] in text.lower():
                if doesStringContainsAll(text.lower().replace(address_dict_long[h], addres_dict_short[h]), allStandardizedDataArray[arrayPosition].lower()) == 1:
                    copy_sheet.write(iterator, 10, allStandardizedDataArray[arrayPosition])
    
            else:
                try:
                    if  doesStringContainsAll("%s %s" % (text.lower(), addres_dict_short[h]), allStandardizedDataArray[arrayPosition].lower()) == 1:
                        copy_sheet.write(iterator, 11, allStandardizedDataArray[arrayPosition])
                        print (allStandardizedDataArray[arrayPosition])
    
                    if  doesStringContainsAll("%s %s" % (text.lower(), address_dict_long[h]), allStandardizedDataArray[arrayPosition].lower()) == 1:
                        copy_sheet.write(iterator, 12, allStandardizedDataArray[arrayPosition])
                        print (allStandardizedDataArray[arrayPosition])
                except:
                    pass
                    print ("Failed on %s" % allStandardizedDataArray[arrayPosition])
    
    
    
    
    
    
        if maxValue >= 100:
            copy_sheet.write(iterator, 0, allStandardizedDataArray[arrayPosition])
            print (allStandardizedDataArray[arrayPosition])
    
        elif maxValue >= 85:
            copy_sheet.write(iterator, 1, allStandardizedDataArray[arrayPosition])
    
        elif allStandardizedDataArray[arrayPosition] in text or text in allStandardizedDataArray[arrayPosition]:
            copy_sheet.write(iterator, 8, allStandardizedDataArray[arrayPosition])
    
        elif maxValue >= 75:
            copy_sheet.write(iterator, 2, allStandardizedDataArray[arrayPosition])
    
        elif maxValue >= 65:
            copy_sheet.write(iterator, 3, allStandardizedDataArray[arrayPosition])
    
        elif maxValue >= 50:
            copy_sheet.write(iterator, 4, allStandardizedDataArray[arrayPosition])
    
        elif maxValue >= 40:
            copy_sheet.write(iterator, 5, allStandardizedDataArray[arrayPosition])
    
    
    copy_sheet.write(0, 0, "100% Match")
    copy_sheet.write(0, 1, "99-85% Match")
    copy_sheet.write(0, 2, "84-75% Match")
    copy_sheet.write(0, 3, "74-65% Match")
    copy_sheet.write(0, 4, "64-50% Match")
    copy_sheet.write(0, 5, "49-40% Match")
    copy_sheet.write(0, 6, "Contains all letters")
    copy_sheet.write(0, 7, "Contains all letters (Reversed)")
    copy_sheet.write(0, 8, "Contains String")
    copy_sheet.write(0, 9, "Dictionary Switched")
    copy_sheet.write(0, 10, "Dictionary Switched ex")
    copy_sheet.write(0, 11, "Dictionary Added ex")
    copy_sheet.write(0, 12, "Dictionary Added long ex")
    
    copy_book.save("%s\matching.xls" % saveDirectory)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
