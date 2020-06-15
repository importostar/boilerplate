---
title: username_creator
date: 2020-05-07
---
Example Python program username_creator.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import *
* from tkinter import messagebox

## Classes

* class UsernameWindow:

## Methods

* def __init__(self, appUsername):
* def createUsername(self):

## Code

Python tkinter example

    # Realeased under the MIT Licence
    
    import tkinter
    from tkinter import *
    from tkinter import messagebox
    
    class UsernameWindow:
        def __init__(self, appUsername):
            #Add some text:
            self.firstTitle = tkinter.Label(appUsername, text="First Name:", font=('Helvetica', 10))
            self.firstTitle.grid(row=1, column=0, padx=7.5, pady=7.5)
            
            self.first = Entry(appUsername)
            self.first.grid(row=1, column=1, padx=7.5, pady=7.5)
            self.first.focus_set()
            
            self.lastTitle = tkinter.Label(appUsername, text="Last Name:", font=('Helvetica', 10))
            self.lastTitle.grid(row=2, column=0, padx=7.5, pady=7.5)
            
            self.last = Entry(appUsername)
            self.last.grid(row=2, column=1, padx=7.5, pady=7.5)
    
            self.ageTitle = tkinter.Label(appUsername, text="Your Age:", font=('Helvetica', 10))
            self.ageTitle.grid(row=3, column=0, padx=7.5, pady=7.5)
            
            self.age = Entry(appUsername)
            self.age.grid(row=3, column=1, padx=7.5, pady=7.5)
            
            self.buttonSubmit = Button(appUsername, text="Create", command=self.createUsername)
            self.buttonSubmit.grid(row=4, column=0, columnspan=2, padx=7.5, pady=7.5)
    
    
    
        def createUsername(self):
            firstName = self.first.get().replace(" ", "") #Sets variable & Removes any spaces! [[But abit glitchy if space is in the middle of a word :?]] FIXED!! Now removes spaces within the middle! :D
            lastName = self.last.get().replace(" ", "")
            userAge = self.age.get().replace(" ", "")
            
            firstName = firstName[:4]
            lastName = lastName[-3:]
            userAge = userAge[:2]
            FINAL = firstName+lastName+userAge
    
            if len(self.first.get()) < 4:
                try:
                    self.txt.destroy() #Refreshes
                except:None
                print("No first name")
                self.txt = tkinter.Label(text="Please enter your first name. 4+ Characters.", font=('Helvetica', 10))
                self.txt.grid(row=0, column=0, columnspan=2, padx=7.5, pady=7.5)
    
            elif len(self.last.get()) < 3:
                try:
                    self.txt.destroy() #Refreshes
                except:None
                print("No last name")
                self.txt = tkinter.Label(text="Please enter your last name. 3+ Characters.", font=('Helvetica', 10))
                self.txt.grid(row=0, column=0, columnspan=2, padx=7.5, pady=7.5)
    
            elif len(self.age.get()) == 0:
                try:
                    self.txt.destroy() #Refreshes
                except:None
                print("No age")
                self.txt = tkinter.Label(text="Please enter your age.", font=('Helvetica', 10))
                self.txt.grid(row=0, column=0, columnspan=2, padx=7.5, pady=7.5)
    
            else:
                try:
                    self.txt.destroy() #Refreshes
                except:None
                self.txt = tkinter.Label(text=FINAL, font=('Helvetica', 10))
                self.txt.grid(row=0, column=0, columnspan=2, padx=7.5, pady=7.5)
                try:        
                    toFile = open("usernames.txt", "a")
    
                    toFile.write("Username: "+FINAL+"\n")
    
                    toFile.close()
                except: ## Incase of unknow errors occuring to protect the file
                    messagebox.showinfo("Eh?", "ERROR: An unknow error occured.")
                    print ("\tERROR: An unknow error occured.")
                    try:
                        toFile.close()
                    except:
                        messagebox.showinfo("Eh?", "ERROR: Unable to close file, please exit to prevent system errors!!!")
                        print ("\tERROR: Unable to close file, please exit to prevent system errors!!!")
    
    
    
    ## First window to open
    Username = Tk()
    Username.title("Generate Username") # Sets title
    Username.geometry("300x200")
    Username.columnconfigure(0, weight=100)
    Username.columnconfigure(1, weight=100)
    app_Username = UsernameWindow(Username)
    
    mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
