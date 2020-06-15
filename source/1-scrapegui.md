---
title: 1 scrapegui
date: 2020-05-07
---
Example Python program 1-scrapegui.py

## Modules

* from tkinter import *
* from tkinter import ttk
* from scrapeget import *

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    from scrapeget import *
    
    
    root = Tk()  # Makes the basic window
    
    redditFrame = Frame(root).grid(row=0, column=0, sticky=W, padx=100)
    stockFrame = Frame(root).grid(row=0, column=1, sticky=E, padx=100)
    
    redText = StringVar()
    stockText = StringVar()
    
    # Create the reddit label and button
    redditLabel = Label(redditFrame, textvariable=redText).grid(row=1, column=0, sticky=W)
    redditEntry = Entry(redditFrame)
    redditEntry.grid(row=2, column=0, sticky=W)
    redditButton = Button(redditFrame, text='Scrape Reddit').grid(row=3, column=0, sticky=W)
    redditButton.bind("<Button-1", scrapeReddit())
    
    # Create the stock label and button
    stockLabel = Label(stockFrame, textvariable=stockText).grid(row=1, column=1, sticky=E)
    stockEntry = Entry(stockFrame, width=30)
    stockEntry.grid(row=2, column=1, sticky=E)
    stockButton = Button(stockFrame, text='Scrape Stocks').grid(row=3, column=1, sticky=E)
    
    # Setting the text for the labels(Could also do it when creating label)
    redText.set('Scrape a subreddit\'s headlines.\nEnter subreddit name exactly')
    stockText.set('Get the stock market data for companies.\nEnter abbreviations separated by a space.')
    
    root.mainloop()  # Keeps the window open until it is closed.
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
