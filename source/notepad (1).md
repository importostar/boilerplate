---
title: notepad (1)
date: 2020-05-07
---
Example Python program notepad (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from threading import Thread
* #from pynput.keyboard import Controller, Key
* import time
* import tkinter.scrolledtext as vv
* from tkinter import filedialog
* from tkinter import messagebox

## Methods

* def undo():
* def redo(Y):
* def insert(X):
* def Openf():
* def about():
* def savefas():
* def savef():
* def only_save():
* def newf():
* def exxit():
* def runner():
* def make_menu(w):
* def show_menu(e):

## Code

Python tkinter example

    from tkinter import *
    from threading import Thread
    #from pynput.keyboard import Controller, Key
    import time
    import tkinter.scrolledtext as vv
    from tkinter import filedialog
    from tkinter import messagebox
    global saved
    global fileN
    global first
    global existf
    global undoS, redoS
    redoS=['']
    undoS=['']
    
    #Text=''
    
    def undo():
        global undoS, redoS
        print(undoS)
        if len(undoS) > 0:
            if len(undoS) > 1:
                redoS.append(undoS.pop())
            if undoS==[]:
                return ""
            else:
                return undoS[-1]
    
    
    def redo(Y):
        global undoS, redoS
        print(redoS)
        if len(redoS) > 0:
            X= redoS[-1]
            if len(redoS) > 1:
                undoS.append(redoS.pop())
            elif len(redoS)==1:
                return Y
            return X
    
    
    
    
    def insert(X):
        global undoS
        #X=input(Text)
    
        if undoS != []:
            if X != undoS[-1]:
                undoS.append(X)
        else:
            undoS.append(X)
    
    def Openf():
        global fileN, saved, first, existf
        fileO=filedialog.askopenfile(initialdir="/", title="Select file",filetypes=(("text files", "*.txt"), ("all files", "*.*")))
        try:
            if not saved and not first:
                if messagebox.askyesno("TextEditor Prompt", "Do you want to save this file?"):
                    if existf:
                        only_save()
                    else:
                        savefas()
            text_Input.replace("1.0", "end-1c", '')
            text_Input.insert(INSERT, fileO.read())
            fileN = fileO.name
            new.title("TextEditor" + ' - ' + fileN)
            saved = False
            first = False
            existf = True
        except AttributeError:
            H=0
    
    
    def about():
    
        messagebox.showinfo("About us","We are a non-profit Company want to make profit through funds\nand loot u.")
    
    
    def savefas():
        global saved, fileN, first, existf
        try:
            fileO=filedialog.asksaveasfile(initialdir="/", title="Select file",filetypes=(("text files", "*.txt"), ("all files", "*.*")))
            fileO.write(text_Input.get("1.0", "end-1c"))
            fileN = fileO.name
            new.title("TextEditor" + ' - ' + fileN)
            saved=True
            first=False
            existf=True
            return True
        except AttributeError:
            return False
    
    
    
    def savef():
        global saved, fileN, existf
        if not saved:
            savefas()
        elif saved:
            fileO=open(fileN,'w')
            textsave=str(text_Input.get("1.0", 'end-1c'))
            fileO.write(textsave)
            fileO.close()
        existf=True
    
    
    def only_save():
        global fileN, existf
        fileO = open(fileN, 'w')
        textsave = str(text_Input.get("1.0", 'end-1c'))
        fileO.write(textsave)
        fileO.close()
        existf = True
    
    
    def newf():
        global saved, existf, first
        dis = True
        if not first:
            if messagebox.askyesno("TextEditor Prompt","Do you want to save this file?"):
                if existf:
                    only_save()
                    dis=True
                elif first:
                    dis=savefas()
    
            if dis:
                text_Input.replace("1.0", "end-1c", '')
                new.title("TextEditor")
                saved = False
                existf = False
                first=True
    
    
    def exxit():
        global saved, existf, undoS, redoS
        if not (undoS==[''] and redoS==['']):
            if messagebox.askyesno("TextEditor Prompt", "Do you want to save this file?"):
                if existf:
                    only_save()
                else:
                    savefas()
        exit()
    
    
    def runner():
        while True:
            insert(text_Input.get("1.0", "end-1c"))
            time.sleep(1)
    
    
    
    def make_menu(w):
        global the_menu
        the_menu = Menu(w, tearoff=0)
        the_menu.add_command(label="Cut")
        the_menu.add_command(label="Copy")
        the_menu.add_command(label="Paste")
    
    
    def show_menu(e):
        global the_menu
        w = e.widget
        the_menu.entryconfigure("Cut",
        command=lambda: w.event_generate("<<Cut>>"))
        the_menu.entryconfigure("Copy",
        command=lambda: w.event_generate("<<Copy>>"))
        the_menu.entryconfigure("Paste",
        command=lambda: w.event_generate("<<Paste>>"))
    
        the_menu.tk.call("tk_popup", the_menu, e.x_root, e.y_root)
    
    
    first=True
    saved=False
    existf=False
    global the_menu
    #conl=Controller()
    new=Tk()
    new.title("TextEditor")
    X=vv.Frame(master=new, bg="white")
    X.pack(fill='both', expand='yes')
    text_Input=vv.ScrolledText(master=X, wrap=WORD, width=20, height=10, )
    text_Input.pack(padx=10,pady=10, fill=BOTH, expand=True)
    new.protocol('WM_DELETE_WINDOW', exxit)
    menuB = Menu(new)
    make_menu(new)
    text_Input.bind_class("Text", "<Button-3><ButtonRelease-3>", show_menu)
    fileMenu = Menu(menuB, tearoff=0)
    fileMenu.add_command(label='New', command=lambda:newf())
    fileMenu.add_command(label='Open', command=lambda:Openf())
    fileMenu.add_command(label='Save',command=lambda :savef())
    fileMenu.add_command(label='Save as',command=lambda:savefas())
    fileMenu.add_separator()
    fileMenu.add_command(label='Exit', command=lambda: exit())
    menuB.add_cascade(label="File", menu=fileMenu)
    EditMenu = Menu(menuB, tearoff=0)
    #text_Input.bind_class("Text", "<Button-3><ButtonRelease-3>", show_menu)
    EditMenu.add_command(label='Undo', command=lambda: text_Input.replace("1.0", "end-1c", undo()))
    EditMenu.add_command(label='Redo', command=lambda: text_Input.replace("1.0", "end-1c", redo(text_Input.get("1.0", "end-1c"))))
    EditMenu.add_separator()
    #EditMenu.entryconfigure("Cut",command=lambda: w.event_generate("<<Cut>>"))
    EditMenu.add_command(label='Copy')
    EditMenu.entryconfigure("Copy",command=lambda: text_Input.event_generate("<<Copy>>"))
    EditMenu.add_command(label='Cut')
    EditMenu.entryconfigure("Cut", command=lambda: text_Input.event_generate("<<Cut>>"))
    EditMenu.add_command(label='Paste')
    EditMenu.entryconfigure("Paste",command=lambda: text_Input.event_generate("<<Paste>>"))
    EditMenu.add_separator()
    EditMenu.add_command(label='Find')
    EditMenu.add_command(label='Find and replace')
    
    menuB.add_cascade(label='Edit', menu=EditMenu)
    menuB.add_command(label='About', command=lambda: about())
    menuB.add_command(label='test0', command=lambda: print(text_Input.get("1.0", "end-1c")))
    new.config(menu=menuB)
    C=Thread(target=runner)
    C.start()
    P=Thread(target=new.mainloop())
    P.start()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
