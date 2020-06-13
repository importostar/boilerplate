---
title: pygest_3_10
date: 2020-05-07
---
Example Python program pygest_3_10.py


## Classes

* class View():

## Methods

* def configure_inputs(self):

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
            inputs_frame.columnconfigure(2, weight=1)
            inputs_frame.rowconfigure(0, weight=1)
            inputs_frame.rowconfigure(1, weight=1)
    
            filepath_label = tkinter.Label(inputs_frame, text="File Name:", background="black", foreground="white")
            filepath_label.grid(row=0, column=0, sticky='E')
    
            self.file_entry = tkinter.Entry(inputs_frame)
            self.file_entry.bind("<Button-1>", self.chooseFileName)
            self.file_entry.grid(row=0, column=1, sticky=('E', 'W'))
    
            self.radio_var = tkinter.StringVar()
            self.radio_var.set('sha1')
            sha1 = tkinter.Radiobutton(inputs_frame, text="sha1", variable=self.radio_var, value='sha1')
            sha1.grid(row=0, column=2)
    
            digest_label = tkinter.Label(inputs_frame, text="Compare Digest:", background="black", foreground="white")
            digest_label.grid(row=1, column=0,  sticky='E')
    
            self.digest_entry = tkinter.Entry(inputs_frame)
            self.digest_entry.grid(row=1, column=1, sticky=('E', 'W'))
    
            md5 = tkinter.Radiobutton(inputs_frame, text="md5", variable=self.radio_var, value='md5')
            md5.grid(row=1, column=2)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
