---
title: interface
date: 2020-05-07
---
Example Python program interface.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter.ttk import Progressbar
* from tkinter import filedialog
* from tkinter import ttk
* import matplotlib 
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
* from matplotlib.figure import Figure
* from PyQt5 import QtGui, QtCore, QtWidgets
* # import urllib3
* # from bs4 import BeautifulSoup
* import os
* from web_crawler import *

## Methods

* def chooseFile(root):
* def start_job( ):
* def spinbox_change():

## Code

Example Python PyQt program :

    from tkinter import *
    from tkinter.ttk import Progressbar
    from tkinter import filedialog
    from tkinter import ttk
    import matplotlib 
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
    from matplotlib.figure import Figure
    from PyQt5 import QtGui, QtCore, QtWidgets
    # import urllib3
    # from bs4 import BeautifulSoup
    # urllib3.disable_warnings()
    import os
    from web_crawler import *
    #lambda : crawl(fieldURL, 1))
    
        
    
    #depthfield = int(spinDepth.get())
    global fileLoad 
    urls = []
    # Event handling
    def chooseFile(root):
        try:    
                global urls
                url_files = filedialog.askopenfilename(initialdir=os.getcwd())
            
                with open(url_files) as f:
                    for line in f:
                        urls.append( line )
                
                if len( urls ) > 0:
                    buttonStart['state'] = 'normal'
                    i = 0
                    text_url.configure( values=urls)
                    text_url.current(0)
    
        except Exception as exc:
            print( str( exc ) )
    
    
    
    
    
    #**************************** GUI USING TKINTER START ********************************************
    
    root = Tk()
    root.title('Web Crawler')
    root.resizable(width=FALSE, height=FALSE)
    root.geometry('{}x{}'.format(1000, 500)) #width=950, height=500
    
    def start_job( ):
        start_url = url_text.get()
        depth = spinDepth.get()
    
        if len(urls) > 0:
            buttonStop['state'] = 'normal'
    
        crawler = Crawler()
        crawler.set_urls( urls )
        crawler.set_depth( depth )
        crawler.start_crawling()
    
        # After finish, can use the get_pages method to get the page objects crawled
        for page in crawler.get_crawled_pages():
            print( page.get_url() )
            print( page.is_broken_page )
            print( page.uses_google_analytics)
            print( page.uses_ip_anonymization )
            print( page.uses_ip_anonymization_right )
            print( "Number of broken links: " + str( len( page.get_broken_links() ) ))
    
    def spinbox_change():
        _spinDepth = spinDepth.get()
        #print(_spinDepth)
    # Global values of url field and depth combobox
    url_text = StringVar()
    
    
    
    
    #***** Frames ****
    top_frameLeft = Frame(root, bg="#dee1e5", height=100, width=450).grid(row=0,rowspan=10,column=0,columnspan=5, sticky=EW)
    top_frameRight = Frame(root,bg="#dee1e5", height=100, width=450).grid(row=0,rowspan=10,column=5,columnspan=10, sticky=EW)
    left_frame = Frame(root, bg="#848587", height=400, width=500).grid(row=10,rowspan=5,column=0,columnspan=5, sticky=EW)
    right_frame = Frame(root,bg="#848587", height=400, width=500).grid(row=10,rowspan=5,column=5,columnspan=5, sticky=W)
    toolbar_frame = Frame(root) 
    toolbar_frame.grid(row=12,column=6)
    toolbar_frame2 = Frame(root)
    toolbar_frame2.grid(row=12,column=7, padx=2)
    
    
    labelEmpty = Label(root, text="Web Crawler", bg="#484c4c", fg="white").grid(row=1,column=0,sticky=EW, padx=10, pady=2, columnspan=2)
    
    
    labelURL = Label(top_frameLeft, text="Start URL:", bg="#c5c8cc", bd=4).grid(row=2, column=0, sticky=W, pady=5, padx=10)
    #textfieldURL = Entry(top_frameLeft, bd=4, textvariable=url_text)
    #textfieldURL.grid(row=3,column=0, sticky=EW, padx=10,pady=2, columnspan=2)
    text_url = ttk.Combobox( top_frameLeft, state='readonly', values=urls, textvariable=url_text)
    text_url.grid( row=3,column=0, sticky=EW, padx=10,pady=2, columnspan=2)
    
    labelDepth = Label(top_frameLeft, text="Depth of Search:", bg="#c5c8cc", bd=4).grid(row=2, column=2, sticky=W, pady=5)
    spinDepth = Spinbox(top_frameLeft, from_=1, to=100, bd=4, command=spinbox_change)
    spinDepth.grid(row=3, column=2, sticky=W, padx=6, pady=5)
    
    
    buttonStart = Button(top_frameLeft, text="Start", fg="black", bg="#fce9b5", bd=5,state=DISABLED, command= lambda : start_job())
    buttonStart.grid(row=3, column=3, sticky=EW, pady=5)
    buttonStop = Button(top_frameLeft, text="Stop", fg="black", bg="#fce9b5",bd=5, state=DISABLED)
    buttonStop.grid(row=3, column=4, sticky=EW,padx=2, pady=5)
    
    
    fileLabel = Label(top_frameRight, text="Crawl URLs from a file:", bg="#c5c8cc", bd=4).grid(row=2, column=6, sticky=W)
    buttonFile = Button(top_frameRight, text="Chose File...", fg="black", bg="#fce9b5",bd=5, command=lambda: chooseFile(root)).grid(row=3, column=6,sticky=EW)
    #buttonStart2 = Button(top_frameRight, text="Start", fg="black", bg="#fce9b5", bd=5, command= lambda: crawl(fileLoad, 1)).grid(row=3, column=7, sticky=EW)
    #buttonStop2 = Button(top_frameRight, text="Stop", fg="black", bg="#fce9b5",bd=5).grid(row=2, column=7, sticky=EW)
    
    
    labelResults = Label(left_frame, text="Crawl Results: ", bg="#c5c8cc", bd=1, relief=SUNKEN).grid(row=10, column=0, padx=10, pady=2,sticky=W)
    labelGA = Label(left_frame,text="Google Analytics: ", bg="#c5c8cc").grid(row=11, column=0, padx=10, sticky=W)
    labelIPAnon = Label(left_frame,text="Google Analytics IP Anonymization:  ", bg="#c5c8cc").grid(row=12, column=0, padx=10, sticky=W)
    labelParties = Label(left_frame,text="Third Parties:  ", bg="#c5c8cc").grid(row=13, column=0, padx=10,sticky=W)
    labelBrokenLinks = Label(left_frame,text="Broken Links:  ", bg="#c5c8cc").grid(row=14, column=0, padx=10,sticky=W)
    labelTags = Label(left_frame,text="Most used html tags:  ", bg="#c5c8cc").grid(row=15, column=0, padx=10, pady=2,sticky=W)
    labelStatistics = Label(right_frame, text="Statistics: ", bg="#c5c8cc", bd=1, relief=SUNKEN).grid(row=10, column=6, sticky=W)
    
    # ***** Status Bar *******
    
    
    # ********* Separator *******
    separatorLine1 = Canvas(left_frame,width=1, height=50).grid(row=10,column=5)
    separatorLine2 = Canvas(left_frame,width=1, height=50).grid(row=11,column=5)
    separatorLine3 = Canvas(left_frame,width=1, height=50).grid(row=12,column=5)
    separatorLine4 = Canvas(left_frame,width=1, height=50).grid(row=13,column=5)
    separatorLine5 = Canvas(left_frame,width=1, height=50).grid(row=14,column=5)
    separatorLine6 = Canvas(left_frame,width=1, height=50).grid(row=15,column=5)
    separatorLine6 = Canvas(left_frame,width=1, height=50).grid(row=16,column=5)
    
    #***************************************END GUI************************************************
    
    
    #*************************DATA VIZUALIZATION USING MATPLOTLIB**********************************
    # ******* Plot 1 ********
    x = ['Analytics', 'Advertising', 'Other']
    y = [2, 4, 1]
    f = Figure(figsize=(3,3), dpi=60)
    a = f.add_subplot(111)
    a.bar(x, y)
    a.legend()
    canvas = FigureCanvasTkAgg(f, root)
    title1 = "Third Parties"
    a.set_title(title1)
    canvas.get_tk_widget().grid(row=11, column=6)
    canvas.draw()
    toolbar = NavigationToolbar2TkAgg(canvas, toolbar_frame)
    toolbar.update()
    #canvas._tkcanvas.pack()
    
    # ******* Plot 2 ********
    
    
    f1 = Figure(figsize=(3,3), dpi=60)
    a = f1.add_subplot(111)
    a.plot([2,4,6], [5,7,1])
    a.legend()
    canvas = FigureCanvasTkAgg(f1, root)
    title2 = "Google Analytics"
    a.set_title(title2)
    canvas.get_tk_widget().grid(row=11, column=7, padx=10, sticky=W)
    canvas.draw()
    toolbar = NavigationToolbar2TkAgg(canvas, toolbar_frame2)
    toolbar.update()
    #******************************END DATA VIZUALIZATION******************************************
    
    
    
    
    
    root.mainloop()
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
