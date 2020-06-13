---
title: open_file_module
date: 2020-05-07
---
Example Python program open_file_module.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* import please_wait_module
* import time

## Methods

* def exitProgram():
* def enterFile():
* def openFile():

## Code

Python tkinter example

    import tkinter
    import please_wait_module
    import time
    #IF THE FILE IS IN THE SAME DIRECTORY AS YOUR PROGRAM, YOU DON'T NEED TO
    #ENTER THE FULL PATH.
    
    def exitProgram():
        print('Please wait while we shut down the System')
        time.sleep(2)
        exit()
    
    def enterFile():
        file_path = input('enter your file\'s path, then hit enter: ').strip()
        please_wait_module.please_wait()
        with open(file_path, 'r') as system_file:
            contents = system_file.read()
            print(contents)
    
    def openFile():
        tk = tkinter.Tk()
        fileButton = tkinter.Button(tk, text='PRESS\n to open'
                                             ' and display\n'
                                             'the contents of'
                                             ' your file',
                                            command=enterFile)
        fileButton.pack()
        exitButton = tkinter.Button(tk, text='Click to Exit', command=exitProgram)
        exitButton.pack()
        tk.mainloop()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
