---
title: Where_are_you_from_IP
date: 2020-05-07
---
Example Python program Where_are_you_from_IP.py

## Modules

* import json
* from urllib.request import urlopen
* from tkinter import *
* from tkinter import ttk
* from tkinter import messagebox

## Methods

* def calculate(*args):

## Code

Python tkinter example

    import json
    from urllib.request import urlopen
    from tkinter import *
    from tkinter import ttk
    from tkinter import messagebox
    url = 'http://api.db-ip.com/v2/0c5cdae66564ab2c7e6d19d7250f97345a7aabcb/'
    
    def calculate(*args):
      try:
        ipadress = (ip.get())
        b = urlopen(url + ipadress).read().decode('utf-8')
        cal = json.loads(b)['countryName']
        result = (str(cal))
        searching.set(result)
        messagebox.showinfo("Result!!","My hometown is %s" %result)
      except:
        messagebox.showerror("ERROR!!","*.*")
    root = Tk()
    root.title("IP_Countrycode_Search")
    
    mainframe = ttk.Frame(root, padding="4 4 12 12")
    mainframe.grid(column=0, row=0, sticky=(N, W, E, S))
    mainframe.columnconfigure(0, weight=5)
    mainframe.rowconfigure(0, weight=5)
    
    ip = StringVar()
    searching = StringVar()
    
    ip_entry = ttk.Entry(mainframe, width=7, textvariable=ip)
    ip_entry.grid(column=3, row=1, sticky=(W, E))
    
    ttk.Label(mainframe, textvariable=searching).grid(column=3, row=2, sticky=(W, S))
    ttk.Button(mainframe, text="Where are you from?", command=calculate).grid(column=3, row=3, sticky=(W, S))
    ttk.Label(mainframe, text="  Input IP Adress").grid(column=1, row=1, sticky=W)
    ttk.Label(mainframe, text=":").grid(column=2, row=1, sticky=W)
    ttk.Label(mainframe, text="  I'm from....").grid(column=1, row=2, sticky=W)
    ttk.Label(mainframe, text=":").grid(column=2, row=2, sticky=W)
    
    ip_entry.focus()
    root.bind('<Return>', calculate)
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
