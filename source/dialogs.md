---
title: dialogs
date: 2020-05-07
---
Example Python program dialogs.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import Tkinter
* import tkMessageBox

## Methods

* def next1():
* def mark():

## Code

Python tkinter example

    import Tkinter
    import tkMessageBox
    
    total = 0
    EasyBox1 = Tkinter.Tk()
    EasyBox1.geometry("250x200")
    EasyBox1.title("Quesion 1")
    
    EasyBox2 = Tkinter.Tk()
    EasyBox2.geometry("250x200")
    EasyBox2.title("Quesion 2")
    
    ResultBox = Tkinter.Tk()
    ResultBox.geometry("320x260")
    ResultBox.title("Results")
    
    def next1():
        global total
        if not answr1.get(): tkMessageBox.showerror('no answer')
        elif int(answr1.get()) == 8: total += 1
        print "total after 1:",total
        EasyBox1.withdraw()
        EasyBox2.deiconify()
    
    def mark():
        global total
        if not answr2.get(): tkMessageBox.showerror('no answer')
        elif answr2.get() in ["B", "b"]: total += 1
        print "total after 2:", total
        EasyBox2.withdraw()
        LabelName5 = Tkinter.Label(ResultBox, text="Marks : " + str(total), font=("Impact",20))
        LabelName5.grid(row=2,column=0)
        ResultBox.deiconify()
    
    # window 2
    Tkinter.Label (EasyBox1, text="answer:").pack()
    answr1 = Tkinter.Entry (EasyBox1)
    answr1.pack()
    LabelName2 = Tkinter.Label (EasyBox1, text="State the number of edges in a cube")
    LabelName2.grid(row=1,column=0)
    LabelName2.pack()
    
    # window 2
    Tkinter.Label (EasyBox2, text="answer:").pack()
    answr2 = Tkinter.Entry (EasyBox2)
    answr2.pack()
    LabelName2 = Tkinter.Label (EasyBox2, text="What is the place value of the digit 4 in 76421?")
    LabelName2.grid(row=1,column=0)
    LabelName2.pack()
    LabelName2 = Tkinter.Label (EasyBox2, text="A.Thousands B.Hundreds C.Ones D.Tens")
    LabelName2.grid(row=1,column=0)
    LabelName2.pack()
    
    # hide windows
    EasyBox2.withdraw()
    ResultBox.withdraw()
    
    Tkinter.Button(EasyBox1, text="Next", command=next1).pack()
    Tkinter.Button(EasyBox2, text="result", command=mark).pack()
    EasyBox1.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
