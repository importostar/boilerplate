---
title: pygest_3_5
date: 2020-05-07
---
Example Python program pygest_3_5.py


## Classes

* class View():

## Methods

* def configure_inputs(self):
* def chooseFileName(self, event):

## Code

Python tkinter example

    class View():
        """
        The main view class for the PyGest tkinter interface.
        """
        .
        .
        .
        def configure_inputs(self):
            """
            Configure app input objects: file path, hash value, radio buttons.
            """
            logging.info("We're in the configure_inputs method")
            inputs_frame = tkinter.Frame(self.mainframe, background='white', borderwidth=2, relief='flat')
            inputs_frame.grid(row=1, column=0, sticky=('N', 'S', 'E', 'W'))
            inputs_frame.columnconfigure(0, weight=1)
            inputs_frame.columnconfigure(1, weight=1)
            inputs_frame.rowconfigure(0, weight=1)
    
            filepath_label = tkinter.Label(inputs_frame, text="File Name:", background="black", foreground="white")
            filepath_label.grid(row=0, column=0, sticky='E')
    
            self.file_entry = tkinter.Entry(inputs_frame)
            self.file_entry.bind("<Button-1>", self.chooseFileName)
            self.file_entry.grid(row=0, column=1, sticky=('E', 'W'))
    
        def chooseFileName(self, event):
            """
            Controls file path pop up dialog on click of entry field.
            """
            logging.info("Choose File Name method called.")
            filePath = fd.askopenfilename(title="Choose File to Hash")
            logging.info("File path: " + filePath)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
