---
title: screen_blocker
date: 2020-05-07
---
Example Python program screen_blocker.py

## Modules

* from PIL import Image, ImageTk
* 	import Tkinter as tk
* 	import tkinter as tk
* 	import ttk
* 	import tkinter.ttk as ttk

## Classes

* class FullScreenBlocker(tk.Tk):

## Methods

* 	def __init__(self):
* 	def _show_clnt_confg(self):

## Code

Python tkinter example

    from PIL import Image, ImageTk
    
    try:
    	import Tkinter as tk
    except ImportError:
    	import tkinter as tk
    
    try:
    	import ttk
    except ImportError:
    	import tkinter.ttk as ttk
    
    class FullScreenBlocker(tk.Tk):
    	def __init__(self):
    		tk.Tk.__init__(self)
    		self.top=self
    		# no border; full screen
    		self.top.attributes('-fullscreen', 'true')
    		
    		# always on top
    		self.top.attributes('-topmost', 'true')
    		
    		self.geometry("{0}x{1}+0+0".format(self.winfo_screenwidth(), self.winfo_screenheight()))
    		
    		w,h = self.winfo_screenwidth(),self.winfo_screenheight()
    		cv = tk.Canvas(self, width=w, height=h)
    		cv.pack(fill='both', expand='yes')
    		pil_image = Image.open("this_is_my_background.gif")# you can use .gif, .png, .jpg..
    		pil_image2 = pil_image.resize((w,h), Image.ANTIALIAS)   
    		tk_image = ImageTk.PhotoImage(pil_image2)
    		cv.create_image(w//2, h//2, image=tk_image, anchor='center')
    		tk.Button(cv, text="kill me!", command=self.destroy).pack()
    		
    		self.mainloop()
    		
    	def _show_clnt_confg(self):
    		clnt_top = tk.Toplevel(self.top)
    		# always on top
    		clnt_top.attributes('-topmost', 'true')
    		top_ClntLogin = ClntLogin(clnt_top)
    
    fscrnblcker = FullScreenBlocker()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
