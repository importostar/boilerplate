---
title: table
date: 2020-05-07
---
Example Python program table.py

## Modules

* from tkinter import *
* from tkinter import ttk

## Classes

* class Table(ttk.Frame):
* class HidingScrollBar(ttk.Scrollbar):

## Methods

* def __init__(self, master, data=None, *args, **kwargs):
* def drawTable(self, data):
* def createCell(self, row, column, data):
* def updateCell(self, row, column, data):
* def clearTable(self):
* def updateRow(self, row, rowData):
* def addRow(self, rowData):
* def onFrameConfigure(self, event):
* def set(self, lo, hi, *args):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    
    class Table(ttk.Frame):
        """
        Näide kerimisribadega tabeli kohta Canvas, Frame ning Label elemente kasutades
        """
    
        def __init__(self, master, data=None, *args, **kwargs):
            """
            Tabeli loomiseks vajalike elementide algseadistamine
            """
            super().__init__(master, **kwargs)
    
            # Loome Canvas'e, sest see toetab kerimisribasid
            self.canvas = Canvas(self)
            # Canvas võtab tema ümber oleva raami suuruse (sellesama raami, millele ehitame üles oma klassi)
            self.canvas.grid(row=0, column=0, padx=4, pady=4, sticky=N+S+W+E)
            self.columnconfigure(0, weight=1)
            self.rowconfigure(0, weight=1)
    
            # Canvase sisse omakorda loome uue raami, et hakata sellesse paigutama tabelilahtreid
            self.frame = ttk.Frame(self.canvas)
            self.canvas.create_window(0, 0, anchor=N+W, window=self.frame)
            # Kui raami suurus peaks muutuma, anname sellest teada ka Canvasele, et uuendataks kerimisribadega seonduvat
            self.frame.bind('<Configure>', self.onFrameConfigure)
    
            # Kerimisribad ning nendega seotud käskude sidumine Canvasega
            self.verticalScrollbar = HidingScrollBar(self, orient='vertical', command=self.canvas.yview)
            self.horizontalScrollbar = HidingScrollBar(self, orient='horizontal', command=self.canvas.xview)
            self.canvas.configure(yscrollcommand=self.verticalScrollbar.set, xscrollcommand=self.horizontalScrollbar.set)
    
            # Kerimisribade paigutus välimise raami sees
            self.verticalScrollbar.grid(row=0, column=1, sticky=N+S)
            self.horizontalScrollbar.grid(row=1, column=0, sticky=W+E)
            self.columnconfigure(1, weight=0)
            self.rowconfigure(1, weight=0)
    
            # List, mis hoiab lahtreid kujutavaid Label'eid
            self.labels = []
    
            # Kui konstruktor sai andmeid, joonistame nende põhjal tabeli välja
            if data:
                self.drawTable(data)
    
        def drawTable(self, data):
            """
            Tabeli joonistamine kahemõõtmelise massiivi põhjal
            """
    
            # Kustutame kõik olemasolevad lahtreid kujutavad Label'id
            self.clearTable()
    
            # Läbime algandmed ning loome lahtrite Label'eid sisaldava kahemõõtmelise listi
            for rowIndex in range(len(data)):
                self.labels.append([])
                for colIndex in range(len(data[rowIndex])):
                    self.labels[rowIndex].append(None)
                    self.createCell(rowIndex, colIndex, data[rowIndex][colIndex])
    
        def createCell(self, row, column, data):
            """
            Tabelis uue lahtri loomine
            """
            label = ttk.Label(self.frame, text=str(data), borderwidth=1, relief='solid')
            label.grid(row=row, column=column, sticky=N+S+W+E, ipadx=5, ipady=1)
    
            self.labels[row][column] = label
    
        def updateCell(self, row, column, data):
            """
            Tabelis olemasoleva lahtri sisu uuendamine
            """
            self.labels[row][column].configure(text=str(data))
    
        def clearTable(self):
            """
            Tühjendab tabeli andmetest (kustutades lahtreid kujutavad Label elemendid)
            """
            for label in self.labels:
                label.destroy()
    
            self.labels = []
    
        def updateRow(self, row, rowData):
            """
            Uuendab tabeli rida täiesti uute andmetega
            """
            for cell in self.labels[row]:
                cell.destroy()
    
            self.labels[row] = []
    
            for colIndex in range(len(rowData)):
                    self.labels[row].append(None)
                    self.createCell(row, colIndex, rowData[colIndex])
    
        def addRow(self, rowData):
            """
            Lisab tabeli lõppu uue rea
            """
            self.labels.append([])
            for colIndex in range(len(rowData)):
                    self.labels[-1].append(None)
                    self.createCell(len(self.labels)-1, colIndex, rowData[colIndex])
    
        def onFrameConfigure(self, event):
            """
            Kui sisemise raami suurus (tabeli elementide arv või kõrgus-laius) muutub,
            peame Canvasele kerimise toimimiseks andma teada uue ala suuruse
            """
            self.canvas.configure(scrollregion=self.canvas.bbox('all'))
    
    
    class HidingScrollBar(ttk.Scrollbar):
        """
        Kerimisriba, mis end ise ära peidab, kui seda ei vajata
        """
    
        def set(self, lo, hi, *args):
            """
            Kerimisriba parameetrite seadmine koos vajadusel riba peitmise või näitamisega
            """
    
            # Kui element on juba piisavalt suur terve sisu mahutamiseks
            if float(lo) <= 0.0 and float(hi) >= 1.0:
                # ... eemaldame kerimisriba
                self.grid_remove()
            else:
                # Vastasel juhul taastame selle
                self.grid()
    
            super().set(lo, hi, *args)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
