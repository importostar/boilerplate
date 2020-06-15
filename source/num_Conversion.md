---
title: num_Conversion
date: 2020-05-07
---
Example Python program num_Conversion.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter as tk
* from tkinter import*
* import time
* import tkinter as tk
* from tkinter import*
* import time

## Methods

* def Hex(n):
* def Bin(n):
* def Oct(n):
* def main():
* def changeDigit(digit):
* def HEX2():
* def HEX2():
* def HEX2():
* def HEX2():
* def clear_text():
* def HEX2():
* def clear_text():
* def todec():

## Code

Python tkinter example

    '''
    DIFFERENENT METHODS FOR HEXA, OCTA AND BONARY CONVERSION    
    '''       
    
    def Hex(n):
        h = (n % 16)
        hex_nums = "0123456789ABCDEF"
        h1 = n // 16
        if (h1 == 0):
            return hex_nums[h]
        return Hex(h1) + hex_nums[h]
    
    for i in range (0, 255):
         
        print (Hex(i))
    
    
    
    def Bin(n):
        b = (n % 2)
        bin_nums = "01"
        b1 = n // 2
        if (b1 == 0):
            return bin_nums[b]
        return Bin(b1) + bin_nums[b]
    
    for i in range (0, 3):
         
        print (Bin(i))
        
        
        
        
    def Oct(n):
        o_c = (n % 8)
       oct_nums = "01234567"
        o_c1 = n // 8
        if (o_c1 == 0):
            return bin_nums[o_c]
        return Bin(o_c1) + oct_nums[o_c]
    
    for i in range (0, 10):
         
        print (Oct(i))
    
    
    #%%
        '''
        ANOTHER METHOD HEXADECIMALCONVERSION
     '''   
    def main():
        result = int(input("Enter a whole, positive, number to be converted to hexadecimal: "))
        hexadecimal = ""
        while result != 0:
            remainder = changeDigit(result % 16)
            hexadecimal = str(remainder) + hexadecimal
            result = int(result / 16)
        print(hexadecimal)
    
    def changeDigit(digit):
        decimal =     [10 , 11 , 12 , 13 , 14 , 15 ]
        hexadecimal = ["A", "B", "C", "D", "E", "F"]
        for counter in range(7):
            if digit == decimal[counter - 1]:
                digit = hexadecimal[counter - 1]
        return digit
    
    main()
    
    
    
    #%%
    
    '''
    TAKES BASE, RANGE AS INPUT AND CONVERT AT ONCE
    '''
    def HEX2():
        a= int(input('Enter start:\t'))
        e= int(input('Enter end:\t'))
        d= int(input('Enter base:\t'))
        for i in range (a, e):
            b = ""
            while i != 0:
                x = '0123456789ABCDEF'
                c = i % d
                c1 = x[c]
                b = str(c1) +  b
                i = int(i // d)
            print(b)
            
    HEX2()
    
    #%%
    '''
    TAKES ANY DECIMAL NUMBER AND CONVERT TO ANY GIVEN BASE AND THE BASE
    '''
    def HEX2():
        a= int(input('Enter decimal number: \t'))
        d= int(input('Enter expected base: \t'))
        b = ""
        while a != 0:
            x = '0123456789ABCDEF'
            c = a % d
            c1 = x[c]
            b = str(c1) + b
            a = int(a // d)
        print(b)
            
    HEX2()
    
    #%%
    
    '''
    REQUIRES INPUT RANGE
    '''
    def HEX2():
        for a in range (0, 256):
            b = ""
            while a != 0:
                x = '0123456789ABCDEF'
                c = a % 16
                c1 = x[c]
                b = str(c1) + b
                a = int(a // 16)
            print(b)
       
        
    HEX2()
    #%%
    '''
    TAKES JUST THE NUMBER TO CONVERT  AND THE BASE AND DISPLAY ON GUI
    '''
    import tkinter as tk
    from tkinter import*
    import time
    
    def HEX2():
         a = int(name_sE.get())
         d = int(name_sE2.get())
         b = ""
         while a != 0:
            x = '0123456789ABCDEF'
            c = a % d
            c1 = x[c]
            b = str(c1) + b
            a = int(a // d)
        #print(b)
         T.delete(1.0, END)
         T.insert(END, b)
         
    def clear_text():
        name_sE.delete(0, 'end')
        name_sE2.delete(0, 'end')
        return
    
    
    myApp = tk.Tk()
    myApp.title("Designed by Grace Samson (2017)")
    myApp.geometry("500x300+0+0")
    
    Tops =Frame(myApp, width=300, height = 60, bg ="blue", relief=SUNKEN)
    Tops.pack(side = TOP)
    
    f1 =Frame(myApp, width=500, height = 200, relief=SUNKEN)
    f1.pack(side = LEFT)
    f2 =Frame(myApp, width=500, height = 200, relief=SUNKEN)
    f2.pack(side = RIGHT)
            
    d_time = time.asctime(time.localtime(time.time()))
    lbl1= Label(Tops, font=("arial", 14, "bold"), text= "NUMBER SYSTEM CONVERTER", fg="Steel Blue", bd= 10)  
    lbl1.grid(row=0, column=0)
    lbl1= Label(Tops, font=("arial", 8, "bold"), text= d_time, fg="Steel Blue", bd= 10)  
    lbl1.grid(row=1, column=0)
    
    #signup_bt = Button(Tops, text = 'CONVERSION',  font=("arial", 12, "bold"), width = 15, command =conv_detail)
    #signup_bt.grid(row=3, column=1)
        
    inst2  = Label(f1, font=("arial", 12, "bold"), text ='ENTER NUMBER AND BASE FOR CONVERSION', fg ='RED')
    inst2.grid(row = 0, column=0, sticky=E)
    namelbls = Label(f1, font=("arial", 10, "bold"), text ='NUMBER: ')
    namelbls.grid(row = 3, column=0, sticky=W)
    name_sE = Entry(f1)
    name_sE.grid(row = 3, column = 0)
    #name_sE.bind('<Return>', HEX2)
    namelbls2 = Label(f1, font=("arial", 10, "bold"), text ='BASE: ')
    namelbls2.grid(row = 4, column=0, sticky=W)
    name_sE2 = Entry(f1)
    name_sE2.grid(row = 4, column = 0)
    #name_sE2.bind('<Return>', HEX2)
    conv_bt = Button(f1, text = 'CONVERT',  font=("arial", 10, "bold"), width = 10, fg = 'blue', command =HEX2)
    conv_bt.grid(columnspan=2, sticky=W)
    
    reset_bt = Button(f1, text = 'RESET',  font=("arial", 10, "bold"), width = 8, fg = 'blue', command =clear_text)
    reset_bt.grid(columnspan=2, sticky=W)
    
    S = Scrollbar(f2)
    T = Text(f2, height=10, width=50)
    S.pack(side=RIGHT, fill=Y)
    T.pack(side=LEFT, fill=Y)
    S.config(command=T.yview)
    T.config(yscrollcommand=S.set)
    
    ##if __name__ == __"main"__:
    ##        Main()
    
    myApp.mainloop()
    
    
    #%%
    '''
    TAKES BASE, RANGE AS INPUT AND CONVERT AT ONCE WHILE DISPLAYING ON GUI
    '''
    
    ##################################GUI VERSION WITH PYTHON tkinter######################################### 
    import tkinter as tk
    from tkinter import*
    import time
    
    def HEX2():
         a = int(name_sE3.get())
         e = int(name_sE.get())
         d = int(name_sE2.get())
         for i in range (a, e):
             b = ""
             while i != 0:
                x = '0123456789ABCDEF'
                c = i % d
                c1 = x[c]
                b = str(c1) + ',' + b
                i = int(i // d)
             for elem in b:
                 T.insert(END, elem)
                    
        
              
         
    def clear_text():
        name_sE.delete(0, 'end')
        name_sE2.delete(0, 'end')
        name_sE3.delete(0, 'end')
        return
    
    
    myApp = tk.Tk()
    myApp.title("Designed by Grace Samson (2017)")
    myApp.geometry("500x300+0+0")
    
    Tops =Frame(myApp, width=300, height = 60, bg ="blue", relief=SUNKEN)
    Tops.pack(side = TOP)
    
    f1 =Frame(myApp, width=500, height = 200, relief=SUNKEN)
    f1.pack(side = LEFT)
    f2 =Frame(myApp, width=500, height = 200, relief=SUNKEN)
    f2.pack(side = RIGHT)
            
    d_time = time.asctime(time.localtime(time.time()))
    lbl1= Label(Tops, font=("arial", 14, "bold"), text= "NUMBER SYSTEM CONVERTER", fg="Steel Blue", bd= 10)  
    lbl1.grid(row=0, column=0)
    lbl1= Label(Tops, font=("arial", 8, "bold"), text= d_time, fg="Steel Blue", bd= 10)  
    lbl1.grid(row=1, column=0)
    
    #signup_bt = Button(Tops, text = 'CONVERSION',  font=("arial", 12, "bold"), width = 15, command =conv_detail)
    #signup_bt.grid(row=3, column=1)
        
    inst2  = Label(f1, font=("arial", 12, "bold"), text ='ENTER RANGE OF NUMBER FOR CONVERSION', fg ='RED')
    inst2.grid(row = 0, column=0, sticky=E)
    
    namelbls3 = Label(f1, font=("arial", 10, "bold"), text ='START: ')
    namelbls3.grid(row = 3, column=0, sticky=W)
    name_sE3 = Entry(f1)
    name_sE3.grid(row = 3, column = 0)
    #name_sE2.bind('<Return>', HEX2)
    namelbls = Label(f1, font=("arial", 10, "bold"), text ='END: ')
    namelbls.grid(row = 4, column=0, sticky=W)
    name_sE = Entry(f1)
    name_sE.grid(row = 4, column = 0)
    #name_sE.bind('<Return>', HEX2)
    namelbls2 = Label(f1, font=("arial", 10, "bold"), text ='BASE: ')
    namelbls2.grid(row = 5, column=0, sticky=W)
    name_sE2 = Entry(f1)
    name_sE2.grid(row = 5, column = 0)
    #name_sE2.bind('<Return>', HEX2)
    
    conv_bt = Button(f1, text = 'CONVERT',  font=("arial", 10, "bold"), width = 10, fg = 'blue', command =HEX2)
    conv_bt.grid(columnspan=2, sticky=W)
    
    reset_bt = Button(f1, text = 'RESET',  font=("arial", 10, "bold"), width = 8, fg = 'blue', command =clear_text)
    reset_bt.grid(columnspan=2, sticky=W)
    
    S = Scrollbar(f2)
    T = Text(f2, height=10, width=50)
    S.pack(side=RIGHT, fill=Y)
    T.pack(side=LEFT, fill=Y)
    S.config(command=T.yview)
    T.config(yscrollcommand=S.set)
    
    ##if __name__ == __"main"__:
    ##        Main()
    
    myApp.mainloop()
    #%%
    '''
    CONVERTING BACK FROM ANY BASE TO DECIMAL
    '''
    
    s = 0
    a = (input('enter num: ')).upper()
    b = int(input('enter base: ')) 
    for pos, digit in enumerate(a[-1::-1]):
          s=  (int(digit) * (b**pos)) + s
    print(s)
    
    #%%
    '''
    CONVERTING BACK FROM BINARY TO DECIMAL
    '''    
     
    binary = input('enter a number: ')
    b = int(input('enter base: ')) 
    decimal = 0
    for digit in binary:
        decimal = decimal*b + int(digit)
    print(decimal)
     
    
    #%%##########################################################################
    '''
    CONVERTING BACK FROM ANY BASE TO DECIMAL
    ''' 
    #############################################################################
    
    def todec():
        c = int(input('Enter base of the number to convert to decimal:\t')) 
        a = (input('Then enter the number:\t ')).upper()
        b = list(a)
        s = 0
        x = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F']
        for pos, digit in enumerate(b[-1::-1]):
            y = x.index(digit)
            if int(y)/c >= 1:
                    print('Invalid input!!!')
                    break
            s =  (int(y) * (c**pos)) + s
        return (s)
    
    todec()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
