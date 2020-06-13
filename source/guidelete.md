---
title: guidelete
date: 2020-05-07
---
Example Python program guidelete.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter.filedialog import askdirectory
* from tkinter.messagebox import showerror
* import tkinter.ttk as ttk
* import os
* import time
* import calendar

## Classes

* class MainFrame:

## Methods

* def walk_dir(path,daydif,filetype):
* def __init__(self, master):
* def load_dir(self):
* def get_var(self):
* def ok_click(self):

## Code

Python tkinter example

    from tkinter import *
    from tkinter.filedialog import askdirectory
    from tkinter.messagebox import showerror
    import tkinter.ttk as ttk
    import os
    import time
    import calendar
    
    def walk_dir(path,daydif,filetype):
            if os.path.isdir(path) and os.path.exists(path):
                cnt=0
                #this is for counting for prog bar increment
                start_time1 = time.time()
                for dirpath, dirnames, filenames in os.walk(path):
                    for file in filenames:
                        full_file_path = os.path.join(dirpath,file)
                        time_created = time.ctime(os.path.getmtime(full_file_path))
                        seconds_dif = calendar.timegm(time.gmtime()) - os.path.getmtime(full_file_path)
                        days, seconds = divmod(seconds_dif, 24*60*60)
                        if int(days) >= daydif:
                                if file.endswith("." + filetype):
                                     cnt = cnt + 1
                
                print(cnt)
                endtime1 = (time.time() - start_time1)
                #this will be for deleting
                start_time2 = time.time()
                for dirpath, dirnames, filenames in os.walk(path):
                    for file in filenames:
                        
                        full_file_path = os.path.join(dirpath,file)
                        time_created = time.ctime(os.path.getmtime(full_file_path))
                        
                        seconds_dif = calendar.timegm(time.gmtime()) - os.path.getmtime(full_file_path)
                        days, seconds = divmod(seconds_dif, 24*60*60)
                        
                        if int(days) >= daydif:
                                if file.endswith("." + filetype):
                                     print(file)
            else:
                print("["+path+"]" + ' does not exist or is not a valid path')                   
            cnt = 0
    
            print(endtime1)
            print("--- %s seconds ---" % (time.time() - start_time2))
    class MainFrame:
        
        def __init__(self, master):
            self.browseButton = Button(master,text="Browse",command=self.load_dir,width=15).grid(row=0,column=0, sticky=W)
    
            
            self.v = StringVar()
            e = Entry(master, width=65, textvariable=self.v,state=DISABLED)
            e.grid(row=0,column=2)
            self.v.set("")
     
            #combobox test
            self.var = StringVar(master)
            self.var.set("90 days") # initial value
    
            option = OptionMenu(master, self.var, "30 days", "60 days", "90 days")
            option.grid(row=1,column=0)
    
            #file type combobox test
            self.filetype_var = StringVar(master)
            self.filetype_var.set("") # initial value
    
            self.file_option = OptionMenu(master, self.filetype_var, "jpg", "mp3")
            self.file_option.grid(row=1,column=1)
    
            
            #okbutton test 
            button = Button(master, text="OK", command=self.ok_click,width=15)
            button.grid(row=3)
            master.minsize(width=600, height=200)
    
            #prog bar test
            ft = ttk.Frame()
            ft.grid(row=5)
    
            pb_hd = ttk.Progressbar(ft, orient='horizontal', mode='determinate')
            pb_hd.pack(expand=True, fill=BOTH, side=TOP)
            pb_hd.start(50)
    
    
        def load_dir(self):
            dirname = askdirectory()
            if not dirname:
                pass #file upload cancelled
            print("Dir selected: " + dirname)
            self.v.set(dirname)
    
            
        def get_var(self):
            return self.var.get()
    
        def ok_click(self):
            daydif = int(self.get_var()[:2])
            walk_dir(self.v.get(), daydif, self.filetype_var.get() )
        
    if __name__ == "__main__":
        root = Tk()
        b = MainFrame(root)
        root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
