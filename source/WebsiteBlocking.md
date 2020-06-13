---
title: WebsiteBlocking
date: 2020-05-07
---
Example Python program WebsiteBlocking.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import cv2
* import numpy
* import tkinter
* from tkinter import *
* from tkinter import messagebox
* from datetime import datetime as dt

## Methods

* def hello():

## Code

Python tkinter example

    import time
    import cv2
    import numpy
    import tkinter
    from tkinter import *
    from tkinter import messagebox
    from datetime import datetime as dt
    #print(dir(datetime))
    #date_object= datetime.date.today()
    #date_mine=datetime.date(2020, 2, 18)
    #print(date_object)
    #print(date_mine)
    #print(datetime.date.fromtimestamp(1326244364))
    #print(date_object.year)
    #print(time(11, 34, 00))
    #Windows host file path
    hostsPath=r"C:\Windows\System32\drivers\etc\hosts"
    redirect = '127.0.0.1 '
    #adding website to block
    websites=["www.facebook.com","facebook.com","youtube.com","www.youtube.com"]
    print(dt.now().year)
    print(dt.now())
    while True:
        if dt(dt.now().year, dt.now().month, dt.now().day,2) < dt.now() < dt(dt.now().year, dt.now().month, dt.now().day,3):
            print("Sorry Not Allowed...")
            with open(hostsPath, 'r+') as file:
                content = file.read()
                for site in websites:
                    if site in content:
                        pass
                    else:
                        file.write(redirect + " " + site + "\n")
            webbrowser.open("www.facebook.com")
            root = Tk()
            root.geometry("200x200")
            def hello():
                messagebox.showinfo("Say Hello", "Hello")
                messagebox.showinfo("Say Hello", "Hello World")
                hello()
    
    
            B1 = Button(root, text="Say Hello", command=hello, activebackground="green", font="Arial", height="1",
                        justify="left")
            B1.invoke()
            B2 = Button(root, text="Ready", fg='red', activeforeground="blue", bd="5", bg="black")
            B2.place(x=35, y=150)
            B3 = Button(root, text="Go", relief="ridge", state="disabled")
            B3.pack()
    
            B1.place(x=15, y=35)
            root.mainloop()
            
        else:
            with open(hostsPath, 'r+') as file:
                content = file.readlines()
                file.seek(0)
                for line in content:
                    if not any(site in line for site in websites):
                        file.write(line)
                file.truncate()
            print("Allowed access!")
           
        time.sleep(5)
        #Duration during which blocking will be activated
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
