---
title: raspivn_hc05_pc
date: 2020-05-07
---
Example Python program raspivn_hc05_pc.py

## Modules

* import Tkinter
* from Tkinter import *
* import serial

## Methods

* def ketnoi():
* def chonlua():

## Code

Python tkinter example

    import Tkinter
    from Tkinter import *
    import serial
    
    root = Tk()
    root.title("Raspi.vn Dieu khien Pi-HC-05")
    root.geometry("400x200")
    
    #bien luu tru gia tri chon lua 
    var = IntVar()
    content = StringVar()
    Ser = None
    #ham nay tao ket noi Serial khi nhan nut Ket noi
    def ketnoi():
    	global Ser
    	if(len(content.get()) > 0):
    		Ser = serial.Serial(content.get(), 9600, timeout=1)    #Open Serial port voi toc do 9600
    #ham nay gui command cho HC-05 khi chon 1 trong nhung lua chon  
    def chonlua():
    	global Ser
    	if(Ser != None):
    		if(var.get() == 1):
    			Ser.write("BATLED")
    		elif(var.get() == 2):
    			Ser.write("TATLED")
    		elif(var.get() == 3):
    			Ser.write("THOAT")
    		
    
    E1 = Entry(root, textvariable=content)
    E1.pack(fill=X)
    B = Tkinter.Button(root, text ="Ket noi", command = ketnoi)
    B.pack(fill=X)
    R1 = Radiobutton(root, text="BAT LED ", variable=var, value=1, command=chonlua)
    R1.pack(fill=X)
    R2 = Radiobutton(root, text="TAT LED", variable=var, value=2, command=chonlua)
    R2.pack(fill=X)
    R3 = Radiobutton(root, text="THOAT", variable=var, value=3, command=chonlua)
    R3.pack(fill=X)
    
    label = Label(root)
    label.pack()
    root.mainloop()
    #dong cong Serial
    Ser.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
