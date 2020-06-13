---
title: AcidISO
date: 2020-05-07
---
Example Python program AcidISO.py

## Modules

* import os
* from Tkinter import *
* import Tkinter, Tkconstants, tkFileDialog

## Methods

* def pickfile(): 
* def mount():
* def umount():

## Code

Python tkinter example

    #!/usr/bin/python
    #coding: UTF-8
    
    import os
    from Tkinter import *
    import Tkinter, Tkconstants, tkFileDialog
    
    usr = os.getlogin()
    
    root = Tkinter.Tk()
    root.title("AcidISO")
    root.minsize(200,200)
    root.maxsize(200,200)
    root.geometry("200x200")
    img = Tkinter.Image("photo", file="logo1.png")
    root.tk.call('wm','iconphoto',root._w,img)
    texto = Label(root, text="1)- Carregue uma iso\n2)- Clique em montar\n3)- Quando não for utilizar\na iso montada clique\nem desmontar\n")
    texto.pack()
    
    def pickfile(): 
    	root.filename = tkFileDialog.askopenfilename(initialdir = "/",title = "Select file",filetypes = (("iso files","*.iso"),("all files","*.*")))
    
    files = Tkinter.Button(root, text ="Selecionar ISO", command = pickfile)
    
    files.pack()
    
    def mount():
    	dire = '/home/%s/Acidmnt' % usr
    	os.system("mkdir %s" % dire)
    	direiso = root.filename
    	os.system("gksu 'mount -o loop %s %s' " % (direiso,dire))
    	os.system("exit")
    
    mount = Tkinter.Button(root, text ="Montar ISO", command = mount)
    mount.pack()
    
    def umount():
    	os.system("gksu 'umount /home/%s/Acidmnt' " % (usr))
    	os.system("rm -r /home/%s/Acidmnt" % (usr))
    	os.system("exit")
    
    umount = Tkinter.Button(root, text ="Desmontar ISO", command = umount)
    umount.pack()
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
