---
title: WorkTimeWindow
date: 2020-05-07
---
Example Python program WorkTimeWindow.py

## Modules

* import tkinter
* from doctest import master
* import sys
* import time
* from datetime import date

## Methods

* def timer():
* def StopFull():

## Code

Python tkinter example

    import tkinter
    from doctest import master
    import sys
    import time
    from datetime import date
    
    top = tkinter.Tk()
    top.geometry('200x200')
    taskName = tkinter.StringVar()
    var = tkinter.StringVar()
    today = date.today()
    
    seconds = 0
    minutes = 0
    hours = 0
    
    time_start = time.time()
    
    timerStop = True
    def timer():
        global var
        global seconds
        global minutes
        global hours
        global timerStop
        while timerStop == True:
            top.update()
            try:
                sys.stdout.write("\r{hours} Hours {minutes} Minutes {seconds} Seconds".format(minutes=minutes, seconds=seconds, hours=hours))
                sys.stdout.flush()
                time.sleep(1)
                seconds = int(time.time() - time_start) - minutes * 60
                if seconds >= 60:
                    minutes += 1
                    seconds = 0
                if minutes >= 60:
                    hours += 1
                    minutes = 0
    
            except():
                break
            var.set("Godziny: "+str(hours)+" minuty: "+str(minutes)+" sekundy: "+str(seconds))
            
    
    def StopFull():
        global timerStop
        global seconds
        global minutes
        global hours
        global taskName
        global today
        seconds = str(seconds)
        minutes = str(minutes)
        hours = str(hours)
        today = str(today)
        save = open('Work.txt', mode='a')
        save.write('\n Work title: '+ taskName.get() + '\n')
        save.write('Time: '+hours+':'+minutes+':'+seconds+ '\n')
        save.write('Date: '+today)
        save.close()
        timerStop = False
    
    
    Tasktxt = tkinter.Label(top, text="Task Name")
    Tasktxt.pack(side = tkinter.TOP)
    
    taskTextEnty = tkinter.Entry(master, textvariable = taskName , bd = 5)
    taskTextEnty.pack()
    
    timertxt = tkinter.Label(top, textvariable=var)
    timertxt.pack()
    
    StartBut = tkinter.Button(top, text = 'Start', command = timer )
    StartBut.config( width = 15 )
    StartBut.pack()
    
    StopBut = tkinter.Button(top, text = 'Stop', command = StopFull )
    StopBut.config( width = 15 )
    StopBut.pack()
    
    while True:
        top.update()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
