---
title: Contact_Manager
date: 2020-05-07
---
Example Python program Contact_Manager.py

## Modules

* from Tkinter import *
* from tkFileDialog import askopenfile
* import csv
* self.manage.import_data()
*   This manager class imports and edits contact data
*   def import_data(self):

## Classes

* class UI(object):
* class Manager(object):

## Methods

*   def __init__(self):
*   def fix_scrollbars(self, event):
*   def load(self):
*   def sort(self, key_index = 0):
*   def disp_all(self, contacts):
*   def __init__(self):
*   def import_data(self):
*   def sort_data(self, key_index):

## Code

Python tkinter example

    from Tkinter import *
    from tkFileDialog import askopenfile
    import csv
    
    class UI(object):
      def __init__(self):
        #**********************************CREATE INSTANCE OF THE MANAGER CLASS********************************
        self.manage = Manager()
        #*************************************FORMAT TKINTER WINDOW********************************************
        self.master = Tk() #self.master is the root/basic Tkinter window
        self.master.title("Contact Manager Pro")
        self.master.minsize(300,200)
        self.master.geometry("500x500")
        self.master.config(bg="#FFFFFF")
        #**********************************************MENUBAR**************************************************
        menubar = Menu(self.master)
        self.master.config(menu=menubar)
        #Add File Menu
        filemenu = Menu(menubar)
        menubar.add_cascade(label="File", menu=filemenu)
        #Add items to file menu
        filemenu.add_command(label='Load', command = self.load)
        filemenu.add_command(label='New Address')
        filemenu.add_command(label='Search')
        filemenu.add_separator()
        filemenu.add_command(label="Exit", command=self.master.quit)
        #********************************SCROLLING CANVAS WITH A FRAME INSIDE IT*******************************
        ## Grid sizing behavior in window
        self.master.grid_rowconfigure(0, weight=1)
        self.master.grid_columnconfigure(0, weight=1)
        ## Canvas
        self.cnv = Canvas(self.master)
        self.cnv.grid(row=0, column=0, sticky='nswe')
        ## Scrollbars for canvas
        hScroll = Scrollbar(self.master, orient=HORIZONTAL, command=self.cnv.xview)
        hScroll.grid(row=1, column=0, sticky='we')
        vScroll = Scrollbar(self.master, orient=VERTICAL, command=self.cnv.yview)
        vScroll.grid(row=0, column=1, sticky='ns')
        self.cnv.configure(xscrollcommand=hScroll.set, yscrollcommand=vScroll.set)
        ## Frame in canvas
        self.frm = Frame(self.cnv)
        ## This puts the frame in the canvas's scrollable zone
        self.cnv.create_window(0, 0, window=self.frm, anchor='nw')
        self.cnv.bind('<Configure>', self.fix_scrollbars)
        #*************************START TKINTER MAIN LOOP*********************************************
        self.master.mainloop()
      def fix_scrollbars(self, event):
        ## Update display to get correct dimensions
        self.frm.update_idletasks()
        ## Configure size of canvas's scrollable zone
        self.cnv.configure(scrollregion=(0, 0, self.frm.winfo_width(), self.frm.winfo_height()))
      def load(self):
        self.manage.import_data()
        self.disp_all(self.manage.contacts)
      def sort(self, key_index = 0):
        self.manage.sort_data(key_index)
        self.disp_all(self.manage.contacts)
      def disp_all(self, contacts):
        '''
        This function prints a grid of all the contacts given to it.
        '''
        i = 0 #Loop variable
        for head in contacts['headers']:
          Button(self.frm, text=head, bg="#99CC99", command = lambda x=i:self.sort(x)).grid(row=0,column=i, sticky="wens")
          i += 1
        for i in range(len(contacts['data'])):
          for j in range(len(contacts['data'][i])):
            Label(self.frm, text=contacts['data'][i][j], bg="#FFFFFF", padx="10").grid(row=i+1,column=j, sticky="wens")
    class Manager(object):
      '''
      This manager class imports and edits contact data
      The contact data is stored in the variable self.contacts
      self.contacts is a dictionary of:
        1.headers such as 'name', 'city', 'phone', etc
        2.data for the headers such as 'Elliot', 'DE' etc
      '''
      def __init__(self):
        self.contacts = { 'headers' : [], 'data' : [] }
      def import_data(self):
        '''
        This function opens a csv file and returns a dictionary with headers and data lists.
        '''
        f=askopenfile(mode='rb')
        data = csv.reader(f)
        first = True #Loop variable
        for row in data:
          if first == True:
            self.contacts['headers'].extend(row)
            first = False
          else:
            self.contacts['data'].append(row)
      def sort_data(self, key_index):
        self.contacts['data'].sort(key=lambda x: x[key_index])
    test = UI()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
