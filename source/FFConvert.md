---
title: FFConvert
date: 2020-05-07
---
Example Python program FFConvert.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter,subprocess,os
* from tkinter import filedialog,messagebox
* from tkinter import *

## Classes

* class FFConvert:

## Methods

* def convert(self):
* def fileopen(self):
* def __init__(self):

## Code

Python tkinter example

    #FFPMEG Converter GUI
    import tkinter,subprocess,os
    from tkinter import filedialog,messagebox
    from tkinter import *
    class FFConvert:
        
        def convert(self):
            
            self.btnConvert['state'] = 'disabled'
            self.btn['state']='disabled'
            if self.file:
                self.txt.delete(0.0,END)
                self.txt.insert(0.0,'File: '+self.filename+'\n')
                ext = self.b.getvar(name='contain') #self.container.get()
                self.txt.insert(END,"Converted Container: "+ext+"\n\n Please Wait...")
                print('contain = '+self.b.getvar(name='contain'))
                cmd=subprocess.run("ffmpeg -i \""+self.file.name+"\" -codec copy -y \""+self.file.name+'.'+ext+"\"",shell=True)
                self.txt.insert(END,cmd)
                if cmd.returncode==0:
                    messagebox.showinfo("Done!","Complete")
                    self.txt.delete(0.0,END)
                    self.txt.insert(END,'DONE!')
                    self.btnConvert['state']='normal'
                    self.btn['state']='normal'
                else:
                    messagebox.showerror("ERROR!","Oops, Error X(")
                    self.btn['state']='normal'
                    self.btnConvert['state']='normal'
                print(cmd.stdout)
                print('RESULT: '+str(cmd.returncode))
                
        def fileopen(self):
            
            self.file =  filedialog.askopenfile(filetypes=[('all files', '.*'),('AVI', '.avi'),('MP4','.mp4'),('M4P','.m4p'),('MKV','.mkv'),('WMV','.wmv')])
            if self.file:
                self.filename = self.file.name
                print('File: '+self.filename)
                self.btnConvert['state']='normal'
    
        def __init__(self):
            
            self.gui = Tk()
            self.gui.geometry(newGeometry="300x200")
            self.gui.resizable(width=True, height=True)
            self.gui.title("FFMPEG Converter")
            self.file = None
            self.btn=Button(self.gui,text='Open...',command=self.fileopen)
            self.btn.pack(anchor=E)
            self.container = StringVar()
            self.container.initialize('avi')
            self.container.set('avi')
            self.containers = [("AVI", 'avi'),
                          ("MP4", 'mp4'),
                          ("MKV", 'mkv'),
                          ("WMV", 'wmv'),
                          ("MP3",'mp3'),]  
            for cont, mode in self.containers:
                self.b=Radiobutton(self.gui,indicatoron=1,value=mode,variable='contain',text=cont)
                self.b.pack(anchor=W)
            self.btnConvert = Button(self.gui,text='Convert...',command=self.convert,state='disabled')
            self.btnConvert.pack(anchor=E)
            self.txt=Text(self.gui)
            self.txt.pack(anchor=E)
            self.gui.mainloop()
        
    myConvert = FFConvert()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
