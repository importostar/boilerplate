---
title: extensionchangercomments
date: 2020-05-07
---
Example Python program extensionchangercomments.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* from os import listdir
* from os.path import isfile, join
* import pathlib
* import tkinter as tk
* from tkinter import filedialog

## Methods

* def main():
* def change():

## Code

Python tkinter example

    # Files to change should be in seperate folder
    
    import os
    from os import listdir
    from os.path import isfile, join
    import pathlib
    import tkinter as tk
    from tkinter import filedialog
    # Importing all libraries I will need later
    
    
    def main():
        global onlyfiles
        global folderpath
        global filestarttype
        global fileendtype
        # Set variables as global so other functions can reference them
    
        root = tk.Tk()
        root.withdraw()
    
        filename = filedialog.askdirectory()
        # Displays a GUI that lets the user select a folder
        
        print(filename)
        folderpath = filename
        # Prints the folder path selected, then updates the variable "folderpath" to reflect that
        
        folderpath = os.path.abspath(folderpath)
        # Fixes any potential path errors due to diffrent operating systems.
    
        onlyfiles = [f for f in listdir(folderpath) if isfile(join(folderpath, f))]
        # Sets the variable "onlyfiles" to just the files in the specified folder
    
        print(onlyfiles)
        # Prints the files specified by the "folderpath" folder
    
        cfiles = input("Are these the files you want to use? (y/N) ")
        if (cfiles == "y") or (cfiles == "Y"):
            # looks to see if the "cfiles" user input is yes ("y" or "Y") or no (any other input)
    
            filestarttype = input(
                "What file extension do you want to change? (default is .txt) ") or ".txt"
            fileendtype = input(
                "What file extension is the end result? (default is .bat) ") or ".bat"
            # These variables set what file extensions will be changed based on user input.
            # The "or" statment sets a default value if the user does not add any
    
            change()
            # Calls the "change" function, this is what actually changes the files
    
        else:
            print("Restarting process")
            main()
        # This else statement returns to the top of "main()" and restarts the whole program
        # if the user does not respond with yes to the if statement obove
    
    
    def change():
        global onlyfiles
        # Sets onlyfiles as global so it can be changed near the end of this def
    
        x = -2
        for i in onlyfiles:
            # Runs for as many times as there are files listed in the "onlyfiles" variable
            x = x+1
            if filestarttype in onlyfiles[x]:
                # looks each time it loops to see if that file in the "onlyfiles" array includes
                # the file extension stored in the variable "filestarttype", if yes, it continues,
                # if not it moves on to the next file in the list
    
                os.rename(os.path.join(folderpath, onlyfiles[x]), (os.path.join(
                    folderpath, onlyfiles[x].replace(filestarttype, fileendtype))))
                # This function renames the file to the specified file extension.
                # "os.rename" renames one file to the name of another file.
                # Normally this looks like: os.rename("fileone.xyz", "filetwo.yxz")
    
                # "os.path.join" makes a path to a file out of strings based on the current operating system,
                # this allows the program to run correctly on Windows, Mac, ect.
    
                # In this useage, the first "os.path.join" is joining the path to the selected folder (in "folderpath")
                # with the current file it is changing (stored in "onlyfiles[x]"
                # where x is the number for the current file in the array list)
    
                # The second "os.path.join" is the same for the first part, then used the ".replace" command.
                # This command replaces part of a string with another part (ex replacing ".txt" with ".bat")
    
                # This usage of ".replace" replaces the file extension of the file currently being changed with
                # the file extension it should be changed to
    
        onlyfiles = [f for f in listdir(folderpath) if isfile(join(folderpath, f))]
        # Updates the variable "onlyfile" with the new file names
        print("Done!")
        print(onlyfiles)
        input()
        # Prints "Done!" and the file names after the change, then waits for user input before closing
    
    
    if __name__ == "__main__":
        main()
    # Runs "main()" once the file is run
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
