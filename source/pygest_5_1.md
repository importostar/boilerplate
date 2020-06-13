---
title: pygest_5_1
date: 2020-05-07
---
Example Python program pygest_5_1.py


## Classes

* class View():

## Methods

* def __init__(self, root_object):
* def set_up(self):
* def configure_root(self):
* def configure_mainframe(self):
* def configure_buttons(self):

## Code

Python tkinter example

    class View():
        """
        The main view class for the PyGest tkinter interface.
        """
        def __init__(self, root_object):
            self.root = root_object
            self.mainframe = None
            self.filePath = None
            self.set_up()
    
        def set_up(self):
            """
            Run necessary view and widget configuration methods.
            """
            self.configure_root()
            self.configure_mainframe()
            self.configure_banner()
            self.configure_inputs()
            self.configure_outputs()
            self.configure_buttons()
    
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
            self.mainframe.rowconfigure(0, weight=0)
            self.mainframe.rowconfigure(1, weight=1)
            self.mainframe.rowconfigure(2, weight=1)
            self.mainframe.rowconfigure(3, weight=1)
        .
        .
        .
        def configure_buttons(self):
            """
            Configure button frame and two buttons: hash and clear.
            """
            logging.info("We're in the configure buttons method.")
            buttons_frame = tkinter.Frame(self.mainframe, background="blue", borderwidth=2, relief='flat')
            buttons_frame.grid(row=3, column=0,  sticky=('N', 'S', 'E', 'W'))
            buttons_frame.columnconfigure(0, weight=1)
            buttons_frame.rowconfigure(0, weight=1)
            buttons_frame.rowconfigure(1, weight=1)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
