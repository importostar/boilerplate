---
title: isDropboxRunning
date: 2020-05-07
---
Example Python program isDropboxRunning.py

## Modules

* import tkinter
* from tkinter import messagebox
* import subprocess
* import time

## Code

Python tkinter example

    """
    Simple Python3 script that checks if your Dropbox Linux desktop client is running, and restarts it if it's stopped.
    You may start the script from a systemd unit file, or execute it with another tool on system startup (eg. KDE autostart)
    """
    
    import tkinter
    from tkinter import messagebox
    import subprocess
    import time
    
    sleep_seconds = 30
    
    while True:
    
        time.sleep(sleep_seconds)
        
        output = subprocess.check_output(['ps', '-A'])
    
        if "dropbox" not in str(output):
    
            root = tkinter.Tk()
            root.withdraw()
    
            answer = messagebox.askyesno("Dropbox has stopped!", "Dropbox service has stopped!\nWould you like to restart it?")
            root.destroy()
    
            if answer:
                subprocess.call(['dropbox', 'start'], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
