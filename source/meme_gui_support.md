---
title: meme_gui_support
date: 2020-05-07
---
Example Python program meme_gui_support.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import subprocess
* from os import listdir
* from os.path import isfile, join
* from search import *
* from Tkinter import *
* from tkinter import *
* import ttk
* import tkinter.ttk as ttk
* from PIL import Image, ImageTk
* import meme_gui

## Classes

* class memes:

## Methods

* 	def __init__(self):
* def init(top, gui, *args, **kwargs):
* def destroy_window():
* def getMemeList(query):
* def display(canvas, image_path):
* def settings():
* 	def callback():
* 	def callbackerr():
* def progress(progress_var,MAX):
* def go(canvas, query):
* def next(canvas):
* def prev(canvas):

## Code

Python tkinter example

    import sys
    import subprocess
    from os import listdir
    from os.path import isfile, join
    from search import *
    
    
    try:
        from Tkinter import *
    except ImportError:
        from tkinter import *
    
    try:
        import ttk
        py3 = 0
    except ImportError:
        import tkinter.ttk as ttk
        py3 = 1
    
    from PIL import Image, ImageTk
    
    
    
    class memes:
    	def __init__(self):
    		self.memeList= ['nofile']
    		self.currentImage= 0
    
    m= memes()
    
    
    def init(top, gui, *args, **kwargs):
        global w, top_level, root
        w = gui
        top_level = top
        root = top
    
    def destroy_window():
        # Function which closes the window.
        global top_level
        top_level.destroy()
        top_level = None
    
    def getMemeList(query):
    	source='data2.txt'
    	m.memeList= getScore(create_index(source), generateQuery(query))
    
    
    def display(canvas, image_path):
    	x= Image.open(image_path)
    	gif1 = ImageTk.PhotoImage(image= x.resize((300,300),Image.ANTIALIAS))
    	canvas.create_image(200,150, image = gif1)
    	canvas.gif1=gif1
    
    def settings():
    	# Collecting Subreddits
    	root = Tk()
    	root.title("Settings:User Input")
    	root.geometry("300x100+420+166")
    	label = Label(root, text ="Enter the subreddits, separated by commas")
    	label.pack(side=TOP)
    	e= Entry(root)
    	e.place(relx=0.15, rely=0.20, relheight=0.30
                    , relwidth=0.65)
    	def callback():
    		msg= e.get().split(',')
    		temp1=open('./temp.sh', 'wb')
    		with open('./collect.sh', 'r') as f:
    			for line in f:
    				if line.startswith("python .."):
    					line=line.strip()
    					for i in range(0,len(msg)):
    						line = line + " " + msg[i]
    					line=line+"\n"
    				temp1.write(bytes(line))
    		#temp1.write(bytes("\n chmod a+x temp.sh", "utf-8"))
    		temp1.close()
    		#shutil.move("./temp1.txt", "./temp.sh")
    		subprocess.call("chmod a+x temp.sh", shell=True)
    		subprocess.call("./temp.sh", shell=True) #Calling the collect bash script
    		root.destroy()
    
    	def callbackerr():
    		root.destroy()
    	b = Button(root, text = "COLLECT", command = callback)
    	b.place(relx=0.05, rely=0.7, height=26, width=67)
    	c = Button(root, text = "CLOSE", command = callbackerr)
    	c.place(relx=0.73, rely = 0.7, height=26, width=67)
    
    	root.mainloop()
    
    
    def progress(progress_var,MAX):
        Progress_var=DoubleVar()
        Progress_var.set(progress_var)
        TProgressbar1 = ttk.Progressbar(top ,variable=Progress_var, maximum=MAX )
        TProgressbar1.place(relx=0.05, rely=0.9, relwidth=0.52
                , relheight=0.0, height=19)
        TProgressbar1.configure(length="240")
    
    
    
    def go(canvas, query):
    	getMemeList(query)
    	imageList= m.memeList
    	if imageList!= None:
    		# diplay 1st image
    		display(canvas, imageList[0])
    		print('display done')
            progress(0,len(m.memeList))
    	else:
    		print('No matches')
    
    
    
    
    
    def next(canvas):
    	m.currentImage= (m.currentImage+1)%len(m.memeList)
    	display(canvas, m.memeList[m.currentImage])
        progress(m.currentImage,len(m.memeList))
    
    def prev(canvas):
    	m.currentImage= (m.currentImage-1)%len(m.memeList)
    	display(canvas, m.memeList[m.currentImage])
    
    
    #progress_var=m.currentImage
    #MAX=len(m.memeList)
    
    #self.TProgressbar1 = ttk.Progressbar(top ,variable=progress_var, maximum=MAX )
    #self.TProgressbar1.place(relx=0.05, rely=0.9, relwidth=0.52
    #        , relheight=0.0, height=19)
    #self.TProgressbar1.configure(length="240")
    
    
    
    if __name__ == '__main__':
        import meme_gui
        meme_gui.vp_start_gui()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
