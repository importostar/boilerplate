---
title: Checkin_out
date: 2020-05-07
---
Example Python program Checkin_out.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import ttk
* import tkinter.messagebox
* from time import gmtime, strftime
* import datetime
* import sqlite3
* import random
* import matplotlib
* from matplotlib import pyplot as plt

## Methods

* def add_employee(e):
* def clear_entry(e):
* def add(e):
* def windows_admin(e):
* def login_admin(a):
* def windows_employee_Working(e):
* def select_items(a):
* def DeleteName(e):
* def Show_Graph(a):
* def MedPreview(e):
* def Update_data(a):
* def remove_text_table(e):
* def main_menu():
* def check_in_or_out():
* def CheckID():
* def hideAshow():
* def Reshowinout():
* def refresh_Treeview(e):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    import tkinter.messagebox
    from time import gmtime, strftime
    import datetime
    import sqlite3
    import random
    import matplotlib
    matplotlib.use("TkAgg")
    from matplotlib import pyplot as plt
    
    def add_employee(e):
        global name, last_name, tel, addr, email
        # create variable
        name = StringVar()
        last_name = StringVar()
        tel = StringVar()
        addr = StringVar()
        email = StringVar()
    
        # create widgets
        windows_add_EM = Toplevel(windows)
        text_Lable_add = ["name", "lastname", "Tel", "Address", "Email"]
        text_variable_entry = [name, last_name, tel, addr, email]
        for i, Lable_add in enumerate(text_Lable_add):
            Label(windows_add_EM, text=Lable_add).grid(row=i, column=0)
        for i, text_VE in enumerate(text_variable_entry):
            Entry(windows_add_EM, width=20,
                  textvariable=text_VE).grid(row=i, column=1)
        btn_insert = Button(windows_add_EM, text="insert")
        btn_insert.grid(row=5, column=0)
        btn_insert.bind("<Button-1>", add)
        btn_clear = Button(windows_add_EM, text="clear")
        btn_clear.grid(row=5, column=1)
        btn_clear.bind("<Button-1>", clear_entry)
        windows_add_EM.resizable(0, 0)
    
    
    def clear_entry(e):
        name.set("")
        last_name.set("")
        tel.set("")
        addr.set("")
        email.set("")
    
    
    def add(e):
        database_name = name.get()
        database_last_name = last_name.get()
        database_Tel = tel.get()
        database_address = addr.get()
        database_email = email.get()
        rd_id = random.randint(1, 1000000)
        try:
            sql_check_insert_id = "SELECT ID FROM Employee "
            for row in conn.execute(sql_check_insert_id):
                while(row == rd_id):
                    rd_id = random.randint(1, 10000000)
        except Exception as e:
            print("Error medthod add --> {}".format(e))
    
        if(database_name == '' or database_last_name == '' or database_Tel == '' or database_address == '' or database_email == ''):
            tkinter.messagebox.showinfo("Warning", "Please Fill Up All Boxes")
        else:
            try:
                sql = "INSERT INTO 'Employee' (ID,name,lastname,Address,Email,Tel) VALUES('{}','{}','{}','{}','{}','{}')".format(
                    rd_id, database_name, database_last_name, database_address, database_email, database_Tel)
                c.execute(sql)
                conn.commit()
                refresh_Treeview(e)
                tkinter.messagebox.showinfo("insert Successful", "")
                clear_entry(e)
            except Exception as e:
                print("Error add Employee to db --> {}".format(e))
    
    
    def windows_admin(e):
        global id_admin, pass_admin
        id_admin = StringVar()
        pass_admin = StringVar()
        windows_ad = Toplevel(windows)
        Label(windows_ad, text="Admin").grid(column=2)
        Label(windows_ad, text="ID").grid(row=2, column=1)
        Entry(windows_ad, width=30, textvariable=id_admin).grid(row=2, column=2)
        Label(windows_ad, text="Password").grid(row=3, column=1)
        Entry_pass = Entry(windows_ad, width=30, textvariable=pass_admin)
        Entry_pass.config(show="*")
        Entry_pass.grid(row=3, column=2)
        btn_check = Button(windows_ad, text="Log-in")
        btn_check.grid(column=6)
        btn_check.bind("<Button-1>", login_admin)
    
    def login_admin(a):
        text_admin_id = id_admin.get()
        text_admin_pass = pass_admin.get()
        try:
            con_admin.row_factory = sqlite3.Row
            sql_Admin = "SELECT * FROM {} WHERE ID = '"'{}'"' ".format(
                'List_admin', text_admin_id)
            for row in con_admin.execute(sql_Admin):
                text_pass = row["Password"]
                if text_admin_pass == text_pass:
                    tkinter.messagebox.showinfo(
                        "Log-in Successful", "Welcome to Admin Page")
                    windows_employee_Working(a)
                else:
                    tkinter.messagebox.showinfo(
                        "Warning", "The email or password is incorrect")
        except Exception as e:
            print("Error login admin{}".format(e))
    
    
    def windows_employee_Working(e):
        global x, tree, checkbtn, text_tree_col
        windows_Em = Toplevel(windows)
        text_list = ['work first', 'work late', 'out first', 'out late']
        Label(windows_Em, text="list of employee to working").pack()
        # create TreeView by ttk module
        tree = ttk.Treeview(windows_Em)
        tree["columns"] = ("tree_id", "tree_name", "tree_lastname","tree_addr","tree_email","tree_tel")
        tree.heading("#0", text='')
        tree.column("#0", width=1, anchor="w")
        text_tree_col = ["tree_id", "tree_name","tree_lastname","tree_addr","tree_email","tree_tel"]
        for tree_text_l in text_tree_col:
            tree.column(tree_text_l, anchor='center')
        text_tree_head = ["ID", "name", "lastname","address","email","tel"]
        for i, tree_text_head in enumerate(text_tree_col):
            tree.heading(tree_text_head, text=text_tree_head[i])
        try:
            conn.row_factory = sqlite3.Row
            sqli = "SELECT * FROM Employee"
            for row in conn.execute(sqli):
                tree.insert("", 'end', values=("{}".format(row["ID"]), (row["name"]), (row["lastname"]),(row["Address"]),(row["Email"]),(row["Tel"])))
        except Exception as e:
            print("Error method windows_employee_Working --> {}".format(e))
        btn_preview = Button(windows_Em, text='Preview')
        btn_preview.place(x=350, y=225)
        btn_preview.bind("<Button-1>", MedPreview)
        btn_add = Button(windows_Em, text='Add Employee')
        btn_add.place(x=430, y=225)
        btn_add.bind("<Button-1>", add_employee)
        tree.bind("<ButtonRelease-1>", select_items)
        tree.pack()
        checkbtn = [BooleanVar() for i in text_list]
        for i, TL in enumerate(text_list):
            Checkbutton(windows_Em, text=TL, variable=checkbtn[i]).pack(
                side=LEFT)  # ,variable = checkbnt[i]
        windows_Em.resizable(0, 0)
    
    
    def select_items(a):
        global name_select, lastname_select, tel_select, addr_select, email_select, windows_edit, text_id, Delete_id
        name_select = StringVar()
        lastname_select = StringVar()
        tel_select = StringVar()
        addr_select = StringVar()
        email_select = StringVar()
        windows_edit = Toplevel(windows)
        text_Lable_add = ["name", "lastname", "Tel", "Address", "Email"]
        text_variable_entry = [name_select, lastname_select,
                               tel_select, addr_select, email_select]
        for i, Lable_add in enumerate(text_Lable_add):
            Label(windows_edit, text=Lable_add).grid(row=i, column=0)
        for i, text_VE in enumerate(text_variable_entry):
            Entry(windows_edit, width=20, textvariable=text_VE).grid(row=i, column=1)
        text_id = tree.item(tree.selection()[0])['values'][0]
        try:
            sqli = "SELECT * FROM Employee WHERE ID = {}".format(text_id)
            connect = conn.execute(sqli)
            for row in connect:
                Delete_id = row[0]
                name_select.set("{}".format(row["name"]))
                lastname_select.set("{}".format(row["lastname"]))
                tel_select.set("{}".format(row["Tel"]))
                addr_select.set("{}".format(row["Address"]))
                email_select.set("{}".format(row["Email"]))
        except Exception as e:
            print("Error method select_items --> {}".format(e))
        btn_update = Button(windows_edit, text="Update")
        btn_update.grid(row=5, column=0)
        btn_update.bind("<Button-1>", Update_data)
        btn_delete = Button(windows_edit, text="Delete")
        btn_delete.grid(row=5, column=2)
        btn_delete.bind("<Button-1>", DeleteName)
        btn_delete = Button(windows_edit, text="Show Graph")
        btn_delete.grid(row=5, column=1)
        btn_delete.bind("<Button-1>", Show_Graph)
        # btn_showgraph.bind("<Button-1>",Graph_Wemployee)
    
    
    def DeleteName(e):
        global name, last_name, tel, addr, email
        sql_delete = "DELETE FROM Employee WHERE ID = {}".format(Delete_id)
        conn.execute(sql_delete)
        conn.commit()
        refresh_Treeview(e)
    
    
    def Show_Graph(a):
        x = []
        y = []
        sql_x = "SELECT * FROM time_of_employee"
        for row in con_check_time.execute(sql_x):
            x.append(row[2])
            y.append(row[4])
        plt.plot(["4/06/2018", "5/06/2018", "6/06/2018", "7/06/2018",
                  "8/06/2018", "9/06/2018", "10/06/2018"], [9.17, 8, 7, 9.24, 10, 11, 9])
        plt.xlabel('Time')
        plt.ylabel('Date')
        plt.show()
    
    
    def MedPreview(e):
        c = 0
        for i in range(0, 4):
            if(checkbtn[i].get()):
                c += 1
        remove_text_table(e)
        try:
            if c == 1:
                if checkbtn[0].get():
                    sqli = "SELECT * FROM Employee WHERE Timestart < '9'"  # first work
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[1].get():
                    sqli = "SELECT * FROM Employee WHERE Timestart > 9"  # late work
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[2].get():
                    sqli = "SELECT * FROM Employee WHERE Timeout < 17"  # first out
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[3].get():
                    sqli = "SELECT * FROM Employee WHERE Timeout > 17"  # late out
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
            else:
                if checkbtn[0].get() & checkbtn[1].get():
                    tkinter.messagebox.showinfo(
                        "Warning", "can't show Worklate and Workfirst together")
                    remove_text_table(e)
                elif checkbtn[0].get() & checkbtn[2].get():
                    sqli = "SELECT * FROM Employee WHERE Timestart < 9 AND Timeout < 17"
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[0].get() & checkbtn[3].get():
                    sqli = "SELECT * FROM Employee WHERE Timestart < 9 AND Timeout > 17"
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[1].get() & checkbtn[2].get():
                    sqli = "SELECT * FROM Employee WHERE Timestart > 9 AND Timeout < 17"
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[1].get() & checkbtn[3].get():
                    sqli = "SELECT * FROM Employee WHERE Timestart > 9 AND Timeout > 17"
                    connect = conn.execute(sqli)
                    for row in connect:
                        tree.insert("", 'end', values=("{}".format(
                            row["ID"]), (row["name"]), (row["lastname"]), (row["Timestart"]), (row["Timeout"])))
                elif checkbtn[2].get() & checkbtn[3].get():
                    tkinter.messagebox.showinfo(
                        "Warning", "can't show firstout and lateout together")
                    remove_text_table(e)
    
        except Exception as e:
            print("Error medthod Preview --> {}".format(e))
    
    
    def Update_data(a):
        name_update = name_select.get()
        lastname_update = lastname_select.get()
        tel_update = tel_select.get()
        addr_update = addr_select.get()
        email_update = email_select.get()
        try:
            sql_update = "UPDATE Employee SET name = ""'{}'"" , lastname = ""'{}'"" , Tel = ""'{}'"" , Address = ""'{}'"" ,Email = ""'{}'"" WHERE ID = {} ".format(
                name_update, lastname_update, tel_update, addr_update, email_update, text_id)
            conn.execute(sql_update)
            tkinter.messagebox.showinfo("Update Successful", "")
            refresh_Treeview(a)
        except Exception as e:
            print("Error Update_data {}".format(e))
    
    
    def remove_text_table(e):
        for i in tree.get_children():
            tree.delete(i)
    
    
    def main_menu():
        global btn_check, codename, check_text_inout, text_button_check, Entry_codename,bcheck_in_or_out
        text_button_check = StringVar()
        codename = StringVar()  # ต้องใช้ตัวนี้ในการบอกว่าตัวเเปรเป็น what type
        Label(windows, text="Employee", fg='red').grid(row=1, column=0)
        Label(windows, text="Time: {}".format(Localtime)).grid(row=1, column=1)
        Label(windows, text="Codename").grid(row=2, column=0)
        # เวลาจะดึงไปใช้ต้องใส่ textvariable กำหนดตัวเเปรให้มันด้วย
        Entry_codename = Entry(windows, width=10, textvariable=codename)
        Entry_codename.grid(row=2, column=1)
        Entry_codename.bind("<Return>", (lambda event: hideAshow()))
        btn_check = Button(windows, textvariable=text_button_check)
        btn_check.bind("<Button-1>", CheckID)
        btn_ad = Button(windows, text="Admin")
        btn_ad.grid(row=4, column=1)
        btn_ad.bind("<Button-1>", windows_admin)
    
    def check_in_or_out():
        global bcheck_in_or_out
        sql_check_insertinto = "SELECT * FROM time_of_employee"
        try:
            cct = con_check_time.execute(sql_check_insertinto)
            for row in cct:
                print(row[1])
                if(row[1] == 0):#out
                    bcheck_in_or_out = True
                else:
                    bcheck_in_or_out = False
        except Exception as e:
            print("Error Check in or out {}".format(e))
    
    #37269
    def CheckID():
        global bcheck_in_or_out
        bcheck_in_or_out = False
        print("CheckID Worked")
        check_in_or_out()
        try:
            if(bcheck_in_or_out == True):
                        #insert timeout
                print("checkinorout = true")
                sql_insert_timeout = "UPDATE time_of_employee SET time_out = {} , Cinout = 1 WHERE ID = {} AND date_time_em = {}".format(str_time,codename.get(),str_date)
                con_check_time.execute(sql_insert_timeout)
                con_check_time.commit()
            else:
                print("checkinorout = false")
                        #insert to in 
                sql_insert_timedb = "INSERT INTO time_of_employee(ID,Cinout,time_in,date_time_em) VALUES({},0,{},{})".format(codename.get(),str_time,str_date)
                con_check_time.execute(sql_insert_timedb)
                con_check_time.commit()
            Reshowinout()
        except Exception as e:
            print("Error Check id --> {}".format(e))
    
    
    def hideAshow():
        global sql_check_inout, Check_ID_B, check_IN,Check_ID_B
        CheckID()
        print("hideAshow worked")
        conn.row_factory = sqlite3.Row
        sql_check_inout = "SELECT * FROM Employee WHERE ID = ""'{}'""".format(codename.get())
        for row in conn.execute(sql_check_inout):
            check_ID = row["ID"]
            if str(check_ID) == codename.get():
                Check_ID_B = True
            else:
                tkinter.messagebox.showinfo("Warning", "ID is Wrong Please try again")
        if codename.get() != '' and Check_ID_B == True:
            try:
                con_check_time.row_factory = sqlite3.Row
                sql_check_inout = "SELECT * FROM time_of_employee WHERE ID = ""'{}'"" AND date_time_em = {} ".format(codename.get(),str_date)
                for row in con_check_time.execute(sql_check_inout):
                    check_IN = row[1]
                    if(check_IN == 0):
                        text_button_check.set("Check-in")
                    else:
                        text_button_check.set("Check-out")
            except Exception as e:
                print("Error hideAshow --> {}".format(e))
            btn_check.grid(row=3, column=1)
        else:
            tkinter.messagebox.showinfo("Warning", "input your ID")
            codename.set('')
    
    def Reshowinout():
        global check_IN
        try:
            con_check_time.row_factory = sqlite3.Row
            sql_check_inout = "SELECT Cinout FROM time_of_employee WHERE ID = '{}' AND date_time_em = {} ".format(codename.get(),str_date)
            for row in con_check_time.execute(sql_check_inout):
                check_IN = row["Cinout"]
                if(check_IN == 0):
                    text_button_check.set("Check-in")
                else:
                    text_button_check.set("Check-out")
        except Exception as e:
            print("Error Reshowinout --> {}".format(e))
    
    
    def refresh_Treeview(e):
        remove_text_table(e)
        try:
            conn.row_factory = sqlite3.Row
            sqli = "SELECT * FROM Employee"
            for row in conn.execute(sqli):
                tree.insert("", 'end', values=("{}".format(
                    row["ID"]), (row["name"]), (row["lastname"]),(row["Address"]),(row["Email"]),(row["Tel"])))
        except Exception as e:
            print("Error refesh --> {}".format(e))
    
    
    if __name__ == '__main__':
        windows = Tk()
        windows.title("Employee System")
        Localtime = strftime("%a, %d %b %Y", gmtime())
        now = datetime.datetime.now()
        str_date = now.strftime("%Y%m%d")
        str_time = now.strftime("%H%M")
        conn = sqlite3.connect('EmployeeDB.db')
        con_admin = sqlite3.connect('Admin.db')
        con_check_time = sqlite3.connect('Time_employee.db')
        c = conn.cursor()
        Check_ID_B = False
        main_menu()
    
    windows.resizable(0, 0)
    windows.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
