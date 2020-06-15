---
title: imgrou
date: 2020-05-07
---
Example Python program imgrou.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os, random, re, urllib.request
* # import tkinter and the fancy ttk theming
* from tkinter import *
* from tkinter.ttk import *
* from PIL import Image, ImageTk

## Classes

* class ImageButton(object):

## Methods

* 	def __init__(self, row, column):
* 	def setImage(self, imageurl, thumburl):
* 	def removeImage(self):
* 	def click(self):
* def normalizeImgur(url):
* def reload():

## Code

Python tkinter example

    # Public Domain
    # python3 imgrou.py
    
    # some configuration
    IMG_ROWS = 3
    IMG_COLS = 3
    CHUNK_SIZE = 512
    REQUEST_URL = "http://reddit.com/domain/i.imgur.com/random/.json"
    SESSION_KEY = "" # look at your request headers on reddit, Cookie "reddit_session"
    
    import os, random, re, urllib.request
    # import tkinter and the fancy ttk theming
    from tkinter import *
    from tkinter.ttk import *
    # Pillow!
    from PIL import Image, ImageTk
    
    root = Tk()
    
    buttons = []
    imageregex = re.compile(r'"url": "([\w.:\-_%\/]+)"')
    thumbregex = re.compile(r'"thumbnail": "([\w.:\-_%\/]+)"')
    imgurregex = re.compile(r'(?:https?\:\/\/)?(?:i\.)?imgur\.com\/(?:[^a]+\/)*(\w{5,7}(?:\.\w+)?)') # ugh
    
    class ImageButton(object):
    	def __init__(self, row, column):
    		self.button = Button(root, text="...", compound="text", command=self.click)
    		self.button.grid(row=x, column=y)
    		self.thumburl = None
    		self.thumb = None
    		self.imageurl = None
    
    	def setImage(self, imageurl, thumburl):
    		self.imageurl = imageurl
    		self.thumburl = thumburl
    
    		print("... Downloading thumbnail")
    		with urllib.request.urlopen(thumburl) as u:
    			data = u.read()
    		print("==> Done!")
    		self.thumb = ImageTk.PhotoImage(data=data)
    		self.button.configure(image=self.thumb, compound="image")
    
    	def removeImage(self):
    		self.imageurl = None
    		self.thumburl = None
    		self.thumb = None
    		self.button.configure(compound="text")
    
    	def click(self):
    		if self.imageurl:
    			os.startfile(self.imageurl)
    
    def normalizeImgur(url):
    	m = imgurregex.match(url)
    	if not m:
    		return
    	else:
    		iid = m.groups()[0]
    		if "." in iid:
    			return "http://i.imgur.com/" + iid
    		else:
    			return "http://i.imgur.com/" + iid + ".png"
    
    def reload():
    	for i,v in enumerate(buttons):
    		thumburl = ""
    
    		print("... Fetching thread ({}/{})".format(i + 1, IMG_COLS * IMG_ROWS))
    		req = urllib.request.Request(REQUEST_URL, headers={
    			"User-Agent": "imgrou 0.1 by nucular_",
    			"Cookie": "reddit_session=" + SESSION_KEY
    		})
    		
    		# small hack to only fetch needed data
    		imagem = None
    		thumbm = None
    		buf = ""
    
    		u = urllib.request.urlopen(req)
    		while True:
    			chunk = u.read(CHUNK_SIZE).decode("utf-8")
    			if chunk:
    				buf += chunk
    			else:
    				break
    			imagem = imageregex.findall(buf)
    			thumbm = thumbregex.findall(buf)
    			if imagem and thumbm:
    				break
    		u.close()
    
    		if imagem and thumbm:
    			imageurl = normalizeImgur(imagem[0])
    			thumburl = thumbm[0]
    
    			if imageurl:
    				for j in buttons:
    					if j.imageurl == imageurl:
    						print("xx> Got same image twice, invalid session key?")
    						return # give up :C
    
    				print("==> Image: \"{}\"\n\r    Thumbnail: \"{}\"\n\r    Bytes read: {}".format(imageurl, thumburl, len(buf)))
    				v.setImage(imageurl, thumburl)
    			else:
    				print("xx> Invalid image URL")
    		else:
    			print("xx> Weird response :(")
    
    for x in range(IMG_COLS):
    	for y in range(IMG_ROWS):
    		buttons.append(ImageButton(x, y))
    
    		if x == 0:
    			root.grid_columnconfigure(y, weight=1)
    	root.grid_rowconfigure(x, weight=1)
    
    reloadbutton = Button(root, text="Reload!", command=reload)
    reloadbutton.grid(row=IMG_ROWS+1, column=0)
    root.grid_rowconfigure(IMG_ROWS+1, weight=1)
    
    root.geometry("{}x{}".format(IMG_COLS * 85, (IMG_ROWS + 1) * 50))
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
