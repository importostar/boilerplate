---
title: pygest_1_5
date: 2020-05-07
---
Example Python program pygest_1_5.py

## Modules

* import tkinter
* import hashlib
* import logging

## Classes

* class View():

## Methods

* def __init__(self, root_object):
* def main():

## Code

Python tkinter example

    """
    pygest.py
    
    A simple Python tkinter GUI application for processing file hashes.
    
    blog.agupieware.com
    """
    
    import tkinter
    import hashlib
    import logging
    
    title = "PyGest"
    
    class View():
        """
        The main view class for the PyGest tkinter interface.
        """
        def __init__(self, root_object):
            self.root = root_object
    
    def main():
        """
        Main function to run the PyGest GUI application.
        """
        logging.basicConfig(format='[%(asctime)s] ln:%(lineno)d %(levelname)s: %(message)s', datefmt='%I:%M:%s', level=logging.DEBUG)
        logging.info('{} app started. Logger running.'.format(title))
    
        # Declare the tkinter Tk() object as root
        root = tkinter.Tk()
    
        # Pass in its title
        root.title(title)
    
        # Pass the root object to our main View() class
        gui = View(root)
    
        # Run the Tk() object's main loop
        root.mainloop()
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
