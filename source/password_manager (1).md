---
title: password_manager (1)
date: 2020-05-07
---
Example Python program password_manager (1).py

## Modules

* from pyDes import *
* import base64
* import tkMessageBox
* import tkSimpleDialog
* import string
* import random
* import Tkinter
* from Tkinter import *
* import clipboard 
* import os

## Methods

* def set_up():
* def create_key():
* def encrypt(paswrd):
* def decrypt(encpass):
* def NewPassword(size=8, chars=string.ascii_uppercase + string.ascii_lowercase + string.digits):
* def savepass(passw):
* def accesspass():
* def output_pass(decpass):

## Code

Python tkinter example

    #End of Module. The following is code that was personally written by me.
    
    from pyDes import *
    import base64
    import tkMessageBox
    import tkSimpleDialog
    import string
    import random
    import Tkinter
    from Tkinter import *
    import clipboard 
    import os
    
    
    pm = Tkinter.Tk()
    pm.wm_title("Enigma Password Manager")
    acc = StringVar()
    accget = StringVar()
    L1 = Label(pm,text="Name the website you need a new password for").grid(row=0)
    L1 = Label(pm,text="Name the website you want to retrieve a password for").grid(row=1)
    E1 = Entry(pm, bd =1, textvariable = acc).grid(row=0, column=1)
    E2 = Entry(pm, bd =1, textvariable = accget).grid(row=1, column=1)
    
    def set_up():
        _here = os.path.dirname(os.path.abspath(__file__))
        filename = os.path.join(_here, 'passfile.txt')
        if os.path.isfile(filename): 
            pass
        else:
            open(filename, 'w')
    
    set_up()
    enc_key = 0
    
    def create_key():
        global enc_key
        _here = os.path.dirname(os.path.abspath(__file__))
        filename = os.path.join(_here, 'checkfile.txt')
        if os.path.isfile(filename):
            enc_key = tkSimpleDialog.askstring( "Enigma Password Manager", "Please enter your encryption key")        
        else:
            chars=string.ascii_uppercase + string.ascii_lowercase + string.digits
            enc_key = str(''.join(random.choice(chars) for x in range(8)))
            tkMessageBox.showinfo( "Enigma Password Manager", "Your unique encryption key has been copied to your clipboard. Please note it down: " + str(enc_key))
    
            clipboard.copy(enc_key)
            open(filename, 'w')
            open("passfile.txt", "w")
            exit()
            
    def encrypt(paswrd):
        k = des(enc_key, padmode=2)
        paswrd = k.encrypt(paswrd)
        asciipas = base64.b64encode(paswrd)
        savepass(asciipas)    
        
    def decrypt(encpass):
        encpass = base64.b64decode(encpass)
        k = des(enc_key, padmode=2)
        encpass = k.decrypt(encpass)
        output_pass(encpass)
        clipboard.copy(encpass)
    
    create_key()         
             
    def NewPassword(size=8, chars=string.ascii_uppercase + string.ascii_lowercase + string.digits):
        u = acc.get()
        if len(u) == 0:
           pass
        else: 
           newpass = str(''.join(random.choice(chars) for x in range(16)))
           clipboard.copy(newpass)
           tkMessageBox.showinfo( "Enigma wants you to know:", "Your password has been saved and has also been copied to your clipboard: " + newpass)
           newpass = encrypt(newpass)  
       
    def savepass(passw):
             f = open("passfile.txt", "a")
             f.write(str(acc.get()) +" "+ str(passw) +"\n")
             f.close()
             
    def accesspass():
        account = str(accget.get())
        for line in reversed(open("passfile.txt", "r").readlines()):
            whole_account = str(account + " ")
            if whole_account in line:
                s = line
                g = s.split()
                relpass = g[-1]
                decrypt(relpass)
                break
            else:
                pass
    def output_pass(decpass):
        account = str(accget.get())
        tkMessageBox.showinfo( "Enigma wants you to know:", "Your password for " + str(account) + " is: " + str(decpass))
    
    B1 = Tkinter.Button(pm, text ="Generate", command = NewPassword).grid(row=0,column=3)
    
    #B1.pack(side = BOTTOM, pady=5)
    
    B2 = Tkinter.Button(pm, text ="Access saved passwords", command = accesspass).grid(row=1,column=3)
    
    #B2.pack(side = BOTTOM)
    
    pm.mainloop()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
