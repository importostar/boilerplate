---
title: registrationwithsql3
date: 2020-05-07
---
Example Python program registrationwithsql3.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* import  sqlite3
* from tkinter import ttk
* import tkinter as tk

## Methods

* def registrationUser():
* def main_screen():

## Code

Python tkinter example

    from tkinter import *
    import  sqlite3
    from tkinter import ttk
    import tkinter as tk
    
    def registrationUser():
    
    
        #================setting up the get command and sql database============#
        Num      = entry_0.get()
        name1    = entry_1.get()
        email    = entry_2.get()
        add      = entry_3.get()
        gender   = var.get()
        location = c.get()
    
    
        #======sqlite3.connect will create a tittle of the datbase===#
        conn = sqlite3.connect('QuarantineRegistraion.db')
    
    
        #===conndition that will create our data base===#
        with conn:
            cursor = conn.cursor()#creating temporary memory for our database
    
        #=========cursor.execute is a command that bind the result of our tkinter GUI
        cursor.execute('CREATE TABLE IF NOT EXISTS RESIDENT (ResidentNumber TEXT, FULLname TEXT, Email TEXT, Address TEXT, Gender TEXT, Location TEXT)')
        cursor.execute('INSERT INTO RESIDENT (ResidentNumber,Fullname, Email, Address, Gender, Location) VALUES(?,?,?,?,?,?)', (Num,name1,email,add,gender,location,))
        conn.commit()#.commit command will end the transaction of our tkinter GUI
    
    
        #=======emptying the datas on the entry field after pressing the submmit button on the main screen=======#
        entry_0.delete(0,END)
        entry_1.delete (0,END)
        entry_2.delete (0,END)
        entry_3.delete (0,END)
        var.set ('')#in intvar .delete will not work so use .set instead
        c.set       ('')#in strvar .delete will not work so use .set instead
    
        #Label(win, text = "Registration Successful!" , fg = "green", font =("Calibre", 11)).place(x = 185, y = 420)
    
        print("Registration Successful")
    
    
    
    def main_screen():
    
        global entry_0, entry_1, entry_2, entry_3, var , c, win,name1 #global variable to use also outside the function
    
    
        #=============================list that use in droplist=======================================#
        loc = ['Abu Dhabi', 'Ajman', 'Dubai', 'Fujairah', 'Ras Al-Khaimah', 'Sharjah', 'Umm Al-Quwain']
    
    
        win = Tk()
    
    
    
        win.geometry("500x500")#size of the window
    
        win.title("Registration Form") # bar title
    
        #=================================Label and Widgets===============================================================#
        label_0 = Label(win, text = "Quarantine Pass Registration", bg= "gray", width ="25", font = ("Calibre", 13 ,"bold"))
        label_0.place(x = 105, y = 23)
    
        label_6= Label(win, text = "Resident No.", width = "20", font = ("Arial", 12, "bold"))
        label_6.place(x = 40, y = 85)
    
        entry_0 = Entry(win, width = 25)
        entry_0.place( x = 200, y = 85)
    
        label_1 = Label(win, text = "Full Name: ", width = "20", font = ("Arial", 12, "bold"))
        label_1.place(x = 40, y = 130)
    
        entry_1 = Entry(win, width = 25)
        entry_1.place(x= 200, y=130)
    
        label_2 = Label(win, text= "Email: ", width="20", font=("Arial", 12, "bold"))
        label_2.place(x=40, y=180)
    
        entry_2 = Entry(win, width = 25)
        entry_2.place( x = 200, y = 180)
    
        label_3 = Label(win, text="Address: ", width="20", font=("Arial", 12, "bold"))
        label_3.place(x=40, y=230)
    
        entry_3 = Entry(win, width = 25)
        entry_3.place(x = 200, y = 230)
    
        label_4 = Label(win, text = "Gender", width = "20", font = ("Arial", 12, "bold"))
        label_4.place(x = 40, y = 280)
        var = IntVar() #in intvar .delete will not work so use .set instead
        Radiobutton(win, text = "Male", font = ("Arial", 12, "bold" ), padx = 5, variable = var, value = 1).place(x = 190, y = 280)
        Radiobutton(win, text = "Female",font=("Arial", 12, "bold"), padx=5, variable=var, value=2).place(x=270, y=280)
        #if you will use radiobutton value will give you the access to switch in different button
    
        label_5 = Label(win, text="Location", width="20", font=("Arial", 12, "bold"))
        label_5.place(x=50, y=323)
    
    
        #===============================setting up the droplist button bar ===============================================#
        c = StringVar() #in strvar .delete will not work so use .set instead
        droplist = OptionMenu(win, c, *loc)
        droplist.config(width=15)
        c.set("Select your Location")
        droplist.place(x=220, y=320)
    
        #==============================================setting up the "submit" button on the last part=====================#
        Button (win, text = "Submit" , width ="20", bg = "brown", fg = "white", command = registrationUser).place(x=180, y=380)
    
        #====focus command so that if you run the code it will automaticaly go to the first entry box ===#
        entry_0.focus()
    
    
        #==loop to continously run the window==#
        win.mainloop()
    
    main_screen()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
