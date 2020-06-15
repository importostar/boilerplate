---
title: scratchMyBum
date: 2020-05-07
---
Example Python program scratchMyBum.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import *
* from tkinter import ttk
* from tkinter import messagebox
* from tkinter import Text, Tk
* import sqlite3
* import csv
* import sys
* from datetime import date, timedelta

## Methods

* def new_query_menu():
* # def character_limit(entry_text):
* def closeQueryScreen():
* def databaseConnect():
* def writeQueryToFile(event=None):
* # def submitQueryToSQL():

## Code

Python tkinter example

    import tkinter
    from tkinter import *
    from tkinter import ttk
    from tkinter import messagebox
    from tkinter import Text, Tk
    import sqlite3
    import csv
    import sys
    from datetime import date, timedelta
    
    
    
    
    
    USERNAME = "POOPYBOI"
    global userQuery
    userQuery = ""
    
    def new_query_menu():
        global new_query_screen
        global new_explanation_textbox
    
        new_query_screen = tkinter.Tk()
        new_query_screen.title("Submit New Query")
        new_query_screen.geometry("800x600")
        new_query_screen.configure(background="grey")
        new_query_screen.resizable(0, 0)
    
        # new_query_screen.grid_rowconfigure(0, weight = 1)
        # new_query_screen.grid_rowconfigure(1, weight=1)
        # new_query_screen.grid_rowconfigure(2, weight=1)
        new_query_screen.grid_columnconfigure(0, weight=1)
        new_query_screen.grid_columnconfigure(1, weight=1)
        new_query_screen.grid_columnconfigure(2, weight=1)
    
        ##the query
        new_query_label = tkinter.Label(new_query_screen, text="Type of query: ", font=("Helvetica", 16), bg="white", fg="black")
        new_query_label.grid(row=0, column=1)
    
        new_query_combobox = ttk.Combobox(new_query_screen,
                                          values=["Technical", "Software", "Hardware", "Request technical support"])
        new_query_combobox.grid(row=0, column=2, pady=20, padx=5)
        new_query_combobox.config(width=30)
        new_query_combobox.current(1)
    
        new_explanation_label = tkinter.Label(new_query_screen, text="Describe the query: ", font=("Helvetica", 16))
        new_explanation_label.grid(row=2, column=1)
    
        new_explanation_textbox = Text(new_query_screen, height=20, width=60)
        new_explanation_textbox.grid(row=3, column=2, pady=10, padx=5)
    
        new_query_exit = Button(new_query_screen, text="Close", bg="white", fg="black", command=closeQueryScreen)
        new_query_exit.grid(row=5, column=1, pady=5, padx=5)
        new_query_exit.config(height=2, width=10)
    
        new_query_submit = Button(new_query_screen, text="Submit", bg="white", fg="black", command=writeQueryToFile)
        new_query_submit.grid(row=5, column=3)
        new_query_submit.bind("<Return>", writeQueryToFile)
    
    
        new_query_screen.mainloop()
    
    
    
    # def character_limit(entry_text):
    #     if len(entry_text.get()) >
    #query form commands
    
    def closeQueryScreen():
        new_query_screen.quit()
        new_query_screen.destroy()
    
    def databaseConnect():
        conn = sqlite3.connect("queries.db")
        cursor = conn.cursor()
        cursor.execute("CREATE TABLE IF NOT EXISTS `query` (query_ID INTEGER PRIMARY KEY AUTOINCREMENT NOT FULL, \
                             username TEXT, submitted_Query TEXT)")
        cursor.execute("SELECT * FROM `query` WHERE `username` = 'user' AND `submitted_Query` = 'query'")
    
        if cursor.fetchone() is None:
            cursor.execute("INSERT INTO `query` (username, submitted_Query) VALUES('user', 'query')")
            cursor.commit()
    
    
    def writeQueryToFile(event=None):
        userQuery = new_explanation_textbox.get('1.0', END)
        messagebox.showinfo("Title", userQuery)
        print(userQuery)
        if userQuery == "":
            new_query_result = tkinter.Label(new_query_screen, text="", font=("Helvetica", 16))
            new_query_result.grid(row=5, column=2)
            new_query_result.config(text="Please enter a query!")
        else:
            txtUserQuery = open("userQueries.txt", "w")
            txtUserQuery.write(userQuery)
            txtUserQuery.close()
    
    
    
    
    
    # def submitQueryToSQL():
    #     global query_id
    #     databaseConnect()
    #
    #     if len(userQuery) <= 50:
    #         new_query_result.config(text="Please write at least 50 characters for your query!", fg="red")
    #     else:
    #         cursor.execute("S")
    
    
    
    
    
    new_query_menu()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
