---
title: college_management_system
date: 2020-05-07
---
Example Python program college_management_system.py

## Modules

* from tkinter import *
* import tkinter
* from PIL import ImageTk, Image
* import pymysql
* from tkinter import messagebox
* from project import main

## Methods

* def exit3():
* def register():
* def click1():
* def login():
* def click2():

## Code

Python tkinter example

    from tkinter import *
    import tkinter
    from PIL import ImageTk, Image
    import pymysql
    from tkinter import messagebox
    
    
    def exit3():
        cms.destroy()
    
    
    def register():
        def click1():
            db = pymysql.connect("localhost", "root", "1234", "cms")
            cursor = db.cursor()
    
            user_name = e1.get()
            user_email = e2.get()
            user_id = e3.get()
            user_password = e4.get()
            user_cof_password = e5.get()
    
            try:
                q1 = "INSERT INTO cms.user(`user_name`,`user_email`,`user_id`,`user_password`,`user_cof_password`) VALUES (%s,%s,%s,%s,%s)"
                cursor.execute(q1, (user_name, user_email, user_id, user_password, user_cof_password))
                if e4.get() != e5.get():
                    messagebox.showwarning('Registration error', 'Password did not match: Please try again...')
                    db.close()
                elif len(e1.get()) == 0:
                    messagebox.showerror('Registration error', "You haven't  filled out name fields: Please try again...")
                    db.close()
                elif len(e2.get()) == 0:
                    messagebox.showerror('Registration error', "You haven't  filled out email fields: Please try again...")
                    db.close()
                elif len(e3.get()) == 0:
                    messagebox.showerror('Registration error',
                                         "You haven't  filled out username fields: Please try again...")
                    db.close()
                else:
                    messagebox.showinfo('Congratulation {}'.format(user_name), 'You have been successfully registered')
                    db.commit()
            except:
                messagebox.showerror('Error', 'Something went wrong please try again!')
            finally:
                register.destroy()
    
        register = tkinter.Tk()
        register.title("Register")
        register.geometry("450x450")
        register.configure(bg="cyan")
        Label(register, text="Register", font=('Time', '20'), fg='gray32', bg='cyan').grid(row=0, column=1, pady=15,
                                                                                           sticky=W)
        Label(register, text="Name:", font=('Time', '15'), bg='cyan').grid(row=2, column=0)
        e1 = Entry(register)
        e1.grid(row=2, column=1)
        Label(register, text="Email:", font=('Time', '15'), bg='cyan').grid(row=3, column=0)
        e2 = Entry(register)
        e2.grid(row=3, column=1)
        Label(register, text="Username:", font=('Time', '15'), bg='cyan').grid(row=4, column=0)
        e3 = Entry(register)
        e3.grid(row=4, column=1)
        Label(register, text="Password:", font=('Time', '15'), bg='cyan').grid(row=5, column=0)
        e4 = Entry(register, show="*")
        e4.grid(row=5, column=1)
        Label(register, text="Confirm Password:", font=('Time', '15'), bg='cyan').grid(row=6, column=0)
        e5 = Entry(register, show="*")
        e5.grid(row=6, column=1)
        Button(register, text="Submit", bg='steel blue', activebackground='spring green', command=click1).grid(row=7,
                                                                                                               column=1)
        register.mainloop()
    
    
    def login():
        def click2():
            db = pymysql.connect("localhost", "root", "1234", "cms")
            cursor = db.cursor()
    
            user_id = e1.get()
            user_password = e2.get()
    
            try:
                q1 = "SELECT * FROM cms.user WHERE (`user_id`)=%s AND (`user_password`)=%s"
                cursor.execute(q1, (user_id, user_password))
                results = cursor.fetchall()
                if len(e1.get()) == 0:
                    messagebox.showerror('Login error', "You haven't  filled out username fields: Please try again...")
                elif len(e2.get()) == 0:
                    messagebox.showerror('Login error', "You haven't  filled out password fields: Please try again...")
    
                for i in results:
                    if i[3] == e1.get() and i[4] == e2.get():
                        messagebox.showinfo("Login info", "Welcome Mr.{}".format(user_id))
                        cms.destroy()
                        from project import main
                    else:
                        pass
    
            except:
                messagebox.showerror('Error', 'Something went wrong please try again...')
            finally:
                login.destroy()
    
        login = tkinter.Tk()
        login.geometry("450x450")
        login.title("Login")
        login.configure(bg="cyan")
        Label(login, text="Login", font=('Time', '20'), fg='gray32', bg='cyan').grid(row=0, column=1, pady=10)
        Label(login, text="Enter Username:", font=('Time', '15'), bg='cyan').grid(row=1, column=0)
        e1 = Entry(login)
        e1.grid(row=1, column=1)
        Label(login, text="Enter Password:", font=('Time', '15'), bg='cyan').grid(row=2, column=0)
        e2 = Entry(login, show="*")
        e2.grid(row=2, column=1)
        Button(login, text="Submit", bg='steel blue',  activebackground='spring green', command=click2).grid(row=3, column=1)
        login.mainloop()
    
    
    cms = tkinter.Tk()
    cms.geometry("1920x1080")
    cms.title("Collage Management System")
    cms.configure(bg="cyan")
    l1 = Label(cms, text="COLLEGE MANAGEMENT SYSTEM", font=('Time', '30'), fg='gray32', bg='cyan').pack()
    img = ImageTk.PhotoImage(Image.open('gllogo.png'))
    panel = tkinter.Label(cms, image=img, bg='cyan')
    panel.pack(side="top", pady=4)
    Label(cms, text="G.L. Bajaj Institute of Technology & Management", font=('Time', '15'), bg='cyan').pack()
    Label(cms, text="Plot No. 2, Knowledge Park III, G. Noida \nDistt. Gautam Budh Nagar, U.P. \nIndia - 201306",
          font=('Time', '10'), bg='cyan').pack()
    b1 = Button(cms, text="Register", width="35", height="5", bg='steel blue', activebackground='spring green',
                command=register).pack(padx=30, pady=15)
    b2 = Button(cms, text="Login", width="35", height="5", bg='steel blue', activebackground='spring green',
                command=login).pack(padx=30, pady=15)
    b3 = Button(cms, text="Exit", width="35", height="2", bg='steel blue', activebackground='spring green',
                command=exit3).pack(padx=30, pady=15)
    cms.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
