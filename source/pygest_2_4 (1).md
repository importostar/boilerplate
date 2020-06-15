---
title: pygest_2_4 (1)
date: 2020-05-07
---
Example Python program pygest_2_4 (1).py

## Modules

* import tkinter
* import hashlib
* import logging

## Classes

* class View():

## Methods

* def __init__(self, root_object):
* def set_up(self):
* def configure_root(self):
* def configure_mainframe(self):
* def configure_banner(self):
* def main():

## Code

Python tkinter example

    """
    pygest.py
    
    A simple Python GUI tutorial application for processing file hashes.
    
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
            self.mainframe = None
            self.set_up()
    
        def set_up(self):
            """
            Run necessary view and widget configuration methods.
            """
            self.configure_root()
            self.configure_mainframe()
            self.configure_banner()
    
        def configure_root(self):
            """
            Configure the root window of the app via the self.root attribute.
            """
            logging.info("configure_root method called...")
            # self.root.minsize(200, 200)
            self.root.columnconfigure(0, weight=1)
            self.root.rowconfigure(0, weight=1)
    
        def configure_mainframe(self):
            """
            Configure the main frame in the root cell with grid geometry manager.
            """
            logging.info("We are in the configure_mainframe method")
            self.mainframe = tkinter.Frame(self.root, background='blue')
            self.mainframe.grid(column=0, row=0, sticky=('N', 'S', 'E', 'W'))
            self.mainframe.columnconfigure(0, weight=1)
            self.mainframe.rowconfigure(0, weight=1)
    
        def configure_banner(self):
            """
            Configure the header banner for the app with a simple tkinter label.
            """
            logging.info("We are in the banner method")
            banner = tkinter.Label(self.mainframe, background='black', text="PyGest Tutorial App", font=('Futura', 32), fg='white')
            banner.grid(row=0, column=0, sticky=('N', 'S', 'E', 'W'), padx=10, pady=10)
    
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
