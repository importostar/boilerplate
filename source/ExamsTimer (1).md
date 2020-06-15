---
title: ExamsTimer (1)
date: 2020-05-07
---
Example Python program ExamsTimer (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import ttk
* from tkinter import font
* from os import system
* import time
* import datetime
* import sys
* import ctypes

## Methods

* def quit(*args):
* def Minimize(*args):
* def AddExam(*args):
* def RemoveExam(*args):
* def EditDuration(*args):
* def Rename(*args):
* def SetExams(*args):
* def update_time():
* def getEnd(start, duration):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    from tkinter import font
    from os import system
    import time
    import datetime
    import sys
    import ctypes
    
    global scrWidth
    global endTime
    global exams
    
    #Get Screen Width for future text formatting
    try:
        user32 = ctypes.windll.user32
        scrWidth=user32.GetSystemMetrics(0)
    except:
        scrWidth=0
    
    def quit(*args):
        Minimize()
        print("\n\n© Néstor Pérez - 2018")
        print("\n\n---------EXIT---------\n")
        if str(input("Are you sure you want to exit? Y/N: ")).upper()=="Y":
            root.destroy()
            system('shutdown -s')
        else:
            SetExams()
    
    def Minimize(*args):
        root.wm_attributes("-topmost", 0)
        root.attributes("-fullscreen", False)
        root.withdraw()
    
    def AddExam(*args):
        Minimize()
        tempExams=[]
        tempDurations=[]
        print("\n\n© Néstor Pérez - 2018")
        print("\n\n---------ADD EXAM---------\n")
        print("Enter exams names, separated from each other by an ENTER. Once you have entered all of them, leave it blank and press ENTER.")
        while True:
            add=str(input("\nExam name: "))
            if not add:
                break
            else:
                add = "• "+add.upper()
                while True:
                    try:
                        length = int(input("Enter length in MINUTES (0 for NONE): "))
                        if length >= 0:
                            tempDurations.append(length)
                            break
                    except:
                        continue
                tempExams.append(add)
        input("Press ENTER to start...")
        StartTime=datetime.datetime.today()
        for i in tempExams:
            exams.append(i)
            startTimes.append(StartTime)
            durations.append(tempDurations[tempExams.index(i)])
        SetExams()
    
    def RemoveExam(*args):
        if len(exams)>0:
            Minimize()
        while True:
            if len(exams)>0:
                print("\n\n© Néstor Pérez - 2018")
                print("\n\n---------DELETE EXAM---------\n")
                for i in exams:
                    print(str(exams.index(i))+" - "+i)
                select=input("\nEnter exam number to delete (BLANK to finish): ")
                if not select:
                    SetExams()
                    break
                try:
                    select=int(select)
                    if select < 0 or select > (len(exams)-1):
                        continue
                    else:
                        del exams[select]
                        del startTimes[select]
                        del durations[select]
                except:
                    continue
            else:
                SetExams()
                break
    
    def EditDuration(*args):
        if len(exams)>0:
            Minimize()
        else:
            return
        while True:
            print("\n\n© Néstor Pérez - 2018")
            print("\n\n---------EDIT DURATION---------\n")
            for i in exams:
                print(str(exams.index(i))+" - "+i+": "+str(durations[exams.index(i)])+" minutes")
            select=input("\nEnter exam to modify (BLANK to finish): ")
            if not select:
                SetExams()
                break
            try:
                select=int(select)
                if select < 0 or select > (len(exams)-1):
                    continue
                else:
                    newDuration=input("Current set length is "+str(durations[select])+" minutes. Enter desired length in MINUTES: ")
                    try:
                        newDuration=int(newDuration)
                        durations[select]=newDuration
                    except:
                        print("\n---------DURATION NOT VALID!---------")
            except:
                print("\n---------NOT VALID!---------")
    
    def Rename(*args):
        if len(exams)>0:
            Minimize()
        else:
            return
        while True:
            print("\n\n© Néstor Pérez - 2018")
            print("\n\n---------RENAME---------\n")
            for i in exams:
                print(str(exams.index(i))+" - "+i[2:])
            select=input("\nEnter exam to rename (BLANK to finish): ")
            if not select:
                SetExams()
                break
            try:
                select=int(select)
                if select < 0 or select > (len(exams)-1):
                    continue
                else:
                    newName="• "+str(input("Current name is "+str(exams[select][2:])+". Enter desired name: ")).upper()
                    
                    exams[select]=newName
            except:
                print("\n---------NOT VALID!---------")
    
    def SetExams(*args):
        out=[]
        for i in exams:
            out.append(i)
            if durations[exams.index(i)]!= 0:
                out.append(" ["+str(getEnd(startTimes[exams.index(i)],durations[exams.index(i)]))+"]\n")
            else:
                out.append("\n")
        if len(exams)==0:
            examsList.set("")
        else:
            examsList.set(''.join(out))
        root.deiconify()
        root.attributes("-fullscreen", True)
        root.focus_force()
        root.lift()
        root.wm_attributes("-topmost", 1)
    
    def update_time():
        now = datetime.datetime.today()#Get current time
        now = now.strftime("%H:%M:%S")#Format time
        time.set(now)#Set display label to current time
        root.after(1000, update_time)# Trigger the countdown after 1000ms
    
    def getEnd(start, duration):
        return ((start+datetime.timedelta(minutes=duration)).strftime("%H:%M:%S"))
    
    # Use tkinter lib for showing the clock
    root = Tk()#Initializes interpreter and creates the root window
    root.attributes("-fullscreen", True)#Set fullscreen?
    root.configure(background='black')#Root window background
    root.bind("x", quit)#Run quit when x pressed
    root.bind("X", quit)#Run quit when X pressed
    root.bind("a", AddExam)#Run AddExam when a pressed
    root.bind("A", AddExam)#Run AddExam when A pressed
    root.bind("d", RemoveExam)#Run RemoveExam when d pressed
    root.bind("D", RemoveExam)#Run RemoveExam when D pressed
    root.bind("e", EditDuration)#Run EditDuration when e pressed
    root.bind("E", EditDuration)#Run EditDuration when E pressed
    root.bind("r", Rename)#Run Rename when r pressed
    root.bind("R", Rename)#Run Rename when R pressed
    root.focus_force()#Call window to be set on top
    root.after(0, update_time)#After 0ms, run update_time
    
    # Clock settings
    fnt = font.Font(family='Helvetica', size=200, weight='bold')#Defines font to be used
    time = StringVar()#Sets txt as a variable string, which can get updated
    clock = ttk.Label(root, textvariable=time, font=fnt, foreground="white", background="black")#Define clock
    clock.place(relx=0.5, rely=0.0, anchor=N)#Place clock on screen
    
    #Center number
    ctrs = ttk.Label(root, text="\t\t\t     XXXXX\t\t|\t    XXXXX\t\t\t\t", font=("Helvetica 35 bold"),foreground="white", background="gray15")
    ctrs.place(relx=0.5, rely=1.0, anchor=S)
    
    # Credits
    credit = ttk.Label(root, text="© Néstor Pérez | 'X' to exit, 'A' to add, 'D' to delete, 'E' to edit, 'R' to rename", font=("Helvetica 15 bold"),foreground="SystemHighlight", background="black")
    credit.place(relx=0.5, rely=0.01, anchor=N)
    
    #Exams and exam times
    examsList = StringVar()
    exams=[]
    startTimes=[]
    durations=[]
    AddExam()
    if scrWidth != 0:
        examsGUI = ttk.Label(root, textvariable=examsList, font=("Helvetica 60"), foreground="white", background="black", wraplength=scrWidth-20)#Define exams list
    else:
        examsGUI = ttk.Label(root, textvariable=examsList, font=("Helvetica 60"), foreground="white", background="black")#Define exams list
    examsGUI.place(relx=0.01, rely=0.28, anchor=NW)#Place list      
    
    root.lift()
    root.focus_force()
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
