---
title: simple_GUI
date: 2020-05-07
---
Example Python program simple_GUI.py

## Modules

* import tkinter as tk
* from tkinter import messagebox
* from tkinter import filedialog

## Methods

* def is_csv():
* def is_finish():
* def get_file_name():
* def calc_tWP_cnt():

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import messagebox
    from tkinter import filedialog
    
    root = tk.Tk()
    explanation = "Magneto: One Click, Do Everything"
    root.title("UI")
    
    
    def is_csv():
        messagebox.showwarning("Warning", "Please select a '*.csv' file")
    
    
    def is_finish():
        messagebox.showinfo("Infomation", "processing finished!")
    
    
    def get_file_name():
        name = filedialog.askopenfilename()
        return name
    
    
    def calc_tWP_cnt():
        criteria = e1.get()
        resolution = e2.get()
        return float(criteria) // float(resolution)
    
    
    tk.Label(
        root,
        compound=tk.CENTER,
        padx=20,
        pady=10,
        fg="Gainsboro",
        bg="black",
        font="Helvetica 30 bold",
        text=explanation).grid(row=1, column=0, columnspan=2)
    
    tk.Label(root, text="").grid(row=2, columnspan=2)
    
    tk.Label(root, text="tWP spec (ns)", compound=tk.RIGHT).grid(row=3)
    tk.Label(root, text="Time division value (ns)", compound=tk.RIGHT).grid(row=4)
    tk.Label(root, text="Interface speed (Mbps)", compound=tk.RIGHT).grid(row=5)
    
    e1 = tk.Entry(root)
    e2 = tk.Entry(root)
    e3 = tk.Entry(root)
    
    e1.grid(row=3, column=1)
    e2.grid(row=4, column=1)
    e3.grid(row=5, column=1)
    
    tk.Label(root, text="").grid(row=6, columnspan=2)
    
    tk.Button(
        root,
        text='Select a csv File',
        bg='CadetBlue4',
        fg='GhostWhite',
        font='Helvetica 20 bold',
        padx=10,
        pady=10,
        width=25,
        height=3,
        command=mark_valid_instruct,
        compound=tk.BOTTOM).grid(row=7, columnspan=2)
    
    tk.Label(root, text="").grid(row=8, columnspan=2)
    
    tk.Button(
        root,
        text="Quit",
        bg='red4',
        fg='GhostWhite',
        font='Helvetica 20 bold',
        padx=10,
        pady=10,
        width=25,
        height=3,
        command=root.destroy).grid(row=9, columnspan=2)
    
    tk.Label(root, text="").grid(row=10, columnspan=2)
    
    
    if __name__ == '__main__':
        tk.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
