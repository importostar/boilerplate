---
title: getpage
date: 2020-05-07
---
Example Python program getpage.py

## Modules

* import tkinter as tk
* from tkinter import ttk
* from tkinter import scrolledtext
* from threading import Thread
* from Url import get_html
* import queue

## Classes

* class Get_Page(tk.Tk):

## Methods

* def __init__(self):
* def _entry_action(self, keyname):
* def create_entry(self):
* def get_frame(self, w=390, h=100):
* def create_text_box(self):

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import ttk
    from tkinter import scrolledtext
    from threading import Thread
    from Url import get_html
    import queue
    
    
    class Get_Page(tk.Tk):
        def __init__(self):
            super().__init__()
            self.geometry('400x350')
            self.create_entry()
            self.create_text_box()
            self.entry_text = "http://google.com"
            self.entry.insert(tk.END, "https://www.w3.org/People/mimasa/test/schemas/rng/xhtml2.rng" )
            self.entry.bind('<Return>', self._entry_action)
         
            self.mainloop()
    
        def _entry_action(self, keyname):
            """
                THREADING
    
            """
            que = queue.Queue()
            link = self.entry.get()
            th = Thread(target=lambda q, url : q.put(get_html(url)), args=(que, link) )
            th.setDaemon(True)
            th.start()
            th.join()
            res = que.get()
            self.scr.insert(tk.END, res)
           
            
           
              
            
    
        def create_entry(self):
            self.entry_text = tk.StringVar()
            fm = ttk.Frame(self ,  width=390, height=100)
            fm['padding'] = (5, 10)
            fm['relief'] = 'sunken'
           
            self.entry = ttk.Entry(fm, textvariable=self.entry_text)
            
            self.entry.config(width=50)
            self.entry.grid(column=0, row=0, columnspan=3 , ipady=3)
    
            fm.grid(column=0, row=0)
            fm.pack()
    
        def get_frame(self, w=390, h=100):
            fm = ttk.Frame(self ,  width=w, height=h)
            fm['padding'] = (5, 10)
            fm['relief'] = 'sunken'
            return fm
    
        def create_text_box(self):
            self.text_entry = tk.StringVar()
            fm = self.get_frame(h=250)
            self.scr = scrolledtext.ScrolledText(fm, 
            height=15, wrap=tk.WORD, undo=True, width=45,
                                pady=2, padx=3)
            self.scr.grid(column=0, row=0, columnspan=3,pady=2, padx=3 )
            fm.pack()
            
    
    if __name__ == '__main__':
        page = Get_Page()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
