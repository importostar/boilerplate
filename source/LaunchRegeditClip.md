---
title: LaunchRegeditClip
date: 2020-05-07
---
Example Python program LaunchRegeditClip.py

## Modules

* import subprocess
* import os
* import sys
* from builtins import str as text
* import _winreg as winreg
* import winreg
* import Tkinter as Tk
* import tkinter as Tk

## Methods

* def main():
* def write_reg_key_lastkey(regpath):
* def getclipboard():
* def silent_launch(command):

## Code

Python tkinter example

    # encoding: utf-8
    
    import subprocess
    import os
    import sys
    from builtins import str as text
    try:
        import _winreg as winreg
    except ImportError:
        import winreg
    
    try:
        import Tkinter as Tk
    except ImportError:
        import tkinter as Tk
    
    REG_KEY = u"Software\\Microsoft\\Windows\\CurrentVersion\\Applets\\Regedit\\"
    
    
    def main():
        mykeypath = ""
    
        if len(sys.argv) <= 1:
            mykeypath = getclipboard()
        else:
            mykeypath = " ".join(sys.argv[1:])
    
        shorthands = {   
            "HKLM": "LOCAL_MACHINE",
            "HKCU": "CURRENT_USER",
            "HKCR": "CLASSES_ROOT",
            "HKCC": "CURRENT_CONFIG",
            "HKU": "USERS"
        }
    
        for shkey in shorthands.keys():
            if mykeypath.startswith(shkey):
                mykeypath = u"HKEY_{}{}".format(shorthands[shkey], mykeypath[len(shkey):])
                break
    
        # mykeypath = text("Computer\\" + mykeypath).encode("UTF8")
        mykeypath = text("Computer\\" + mykeypath)
    
        # print mykeypath
        write_reg_key_lastkey(mykeypath)
        silent_launch(['regedit.exe'])
    
    
    def write_reg_key_lastkey(regpath):
        # # Key(key=HKEY.CURRENT_USER, sub_key='Software')
        reg = winreg.ConnectRegistry(None, winreg.HKEY_CURRENT_USER)
    
        # HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Applets\Regedit
        key = winreg.OpenKey(reg, REG_KEY, 0, winreg.KEY_ALL_ACCESS)
    
        # value = winreg.QueryValueEx(key, u"Lastkey")
        # print (value)
    
        winreg.SetValueEx(key, "Lastkey", 0, winreg.REG_SZ, regpath)
        value = winreg.QueryValueEx(key, u"Lastkey")
        # print (value)
    
    
    def getclipboard():
        try:
            root = Tk.Tk()
            root.withdraw()
            return root.clipboard_get()
        except Tk._tkinter.TclError:
            return ""
    
    
    def silent_launch(command):
        startupinfo = None
        proc = subprocess.Popen(command, startupinfo=startupinfo)
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
