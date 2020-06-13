---
title: inspiration
date: 2020-05-07
---
Example Python program inspiration.py

## Modules

* import tkinter
* import random

## Methods

* def new_inspiration():

## Code

Python tkinter example

    # Inspirational Sayings
    # By @TokyoEdTech YouTube Channel: https://www.youtube.com/channel/UC2vm-0XX5RkWCXWwtBZGOXg
    import tkinter
    import random
    
    root = tkinter.Tk()
    root.title("Inspiration")
    root.geometry("225x75")
    
    lbl_inspiration = tkinter.Label(root, wraplength=200)
    lbl_inspiration.pack()
    
    sayings = [
        "All things are difficult before they are easy. - John Norley",
        "Don't wait. The time will never be just right. - Napoleon Hill",
        "Wherever you go, go with all your heart. - Confucius",
        "Eighty percent of success is showing up. - Woody Allen",
        "A jug fills drop by drop. - Buddha"
    ]
    
    def new_inspiration():
        saying = random.choice(sayings)
        lbl_inspiration["text"] = saying
        root.after(10000, new_inspiration)
        
    new_inspiration()
    
    root.mainloop()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
