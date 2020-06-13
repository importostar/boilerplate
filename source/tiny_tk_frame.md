---
title: tiny_tk_frame
date: 2020-05-07
---
Example Python program tiny_tk_frame.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* import md4cli as cli

## Classes

* class Application(Frame):

## Methods

* def __init__(self, master=None):
* def say_hi(self):
* def createButton(self):
* def createText(self):
* def createEntry(self):
* def run(self):
* def print_contents(self, event):
* def GetSource():
* def show():

## Code

Python tkinter example

    # -*- coding: utf-8 -*-
    #!/usr/bin/env python
    from tkinter import *
    import md4cli as cli
    
    class Application(Frame):
    
        def __init__(self, master=None):
            self.logf = cli._inti_d()
            self.histlog = ""
            for l in open(cli.DEFAULT_LOG,'r'):
                self.histlog += l
            #print self.histlog
            Frame.__init__(self, master)
            self.createText()
    
            self.createEntry()
    
            self.createButton()
            
            self.pack()
    
        def say_hi(self):
            print("hi there, everyone!")
    
        def createButton(self):
            self.QUIT = Button(self)
            self.QUIT["text"] = "QUIT"
            self.QUIT["command"] =  self.quit
            #self.QUIT.pack({"side": "left"})
            self.QUIT.pack(side=LEFT)
    
            self.hi_there = Button(self)
            self.hi_there["text"] = "Hello",
            self.hi_there["command"] = self.say_hi
            #self.hi_there.pack({"side": "left"})
    
        def createText(self):
            self.textArea = Text(self)
            self.textArea.pack(fill=X)
            self.textArea.insert(INSERT,self.histlog)
    
            #self.textArea.pack({"side": "left"})
    
        def createEntry(self):
            self.L1 = Label()
            self.L1["text"] = u"→_→"
            self.L1.pack()
            
            self.entrythingy = Entry()
            self.entrythingy.pack(fill=X)
            # here is the application variable
            self.contents = StringVar()
            # set it to some value
            self.contents.set(u"是也乎,(￣▽￣),现在...")
            # tell the entry widget to watch this variable
            self.entrythingy["textvariable"] = self.contents
    
            # and here we get a callback when the user hits return.
            # we will have the program print out the value of the
            # application variable when the user hits return
            self.entrythingy.bind('<Key-Return>',
                                  self.print_contents)
    
        def run(self):
            while True:
                self.text.insert(END, '...')
                self.root.update()#更新以后才能看到变化
                time.sleep(1)#这里为了快点看到效果，改为了1S输出一次
    
            
        def print_contents(self, event):
            print("hi. contents of entry is now ---->", \
                          self.contents.get())
            _lasted = self.contents.get()
            #print type(_lasted)
            #self.logf.write(_lasted.encode('utf8')+"\n")
            self.logf.write(_lasted+"\n")
            self.textArea.insert(INSERT,"%s\n"%_lasted,'a')
            self.contents.set("")
    
        def GetSource():
            get_window = Tkinter.Toplevel(root)
            get_window.title('Source File?')
            Tkinter.Entry(get_window, width=30,
            textvariable=source).pack()
            Tkinter.Button(get_window, text="Change",
            command=lambda: update_specs()).pack()
    
    def show():
        root = Tk()
        app = Application(master=root)
        app.master.title("My Do-Nothing Application")
        #app.master.maxsize(400, 400)
    
        app.mainloop()
        root.destroy()
    
    if __name__ == '__main__':
        if 1 != len(sys.argv) :
            print('''Usage:
            $ python md4gui.py
                    ''')
        else:
            show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
