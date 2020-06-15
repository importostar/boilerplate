---
title: numpadmadness
date: 2020-05-07
---
Example Python program numpadmadness.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import time
* import tkinter

## Classes

* class NumpadmadnessWindow(tkinter.Tk):

## Methods

* def __init__(self):
* def keyrelease(self, event):
* def keypress(self, event):

## Code

Python tkinter example

    import sys
    import time
    import tkinter
    
    
    class NumpadmadnessWindow(tkinter.Tk):
        def __init__(self):
            super().__init__()
            l = tkinter.Label(self, text="Click here and type keys on your Numpad.\nObserve event codes on standard output.")
            l.pack(padx=50, pady=50)
            self.bind("<KeyPress>", self.keypress)
            self.bind("<KeyRelease>", self.keyrelease)
    
        joystick_keys_sane_platforms = {
            "Control_R": "fire",
            "KP_Insert": "fire",
            "KP_0": "fire",
            "KP_Enter": "fire",
            "Alt_R": "fire",
            "KP_Up": "up",
            "KP_8": "up",
            "KP_Down": "down",
            "KP_2": "down",
            "KP_Left": "left",
            "KP_4": "left",
            "KP_Right": "right",
            "KP_6": "right",
            "KP_Home": "leftup",
            "KP_7": "leftup",
            "KP_Prior": "rightup",
            "KP_9": "rightup",
            "KP_End": "leftdown",
            "KP_1": "leftdown",
            "KP_Next": "rightdown",
            "KP_3": "rightdown"
        }
    
        joystick_keys_osx = {
            524352: "fire",       # R alt
            270336: "fire",       # R control
            5374000: "fire",      # kp 0
            498073: "fire",       # kp Enter
            5963832: "up",        # kp 8
            5505074: "down",      # kp 2
            5636148: "left",      # kp 4
            5767222: "right",     # kp 6
            5832759: "leftup",    # kp 7
            6029369: "rightup",   # kp 9
            5439537: "leftdown",  # kp 1
            5570611: "rightdown", # kp 3
        }
    
        joystick_keys_windows_keysym_num = {
            65379: "fire",      # kp 0
            65362: "up",        # kp 8
            65364: "down",      # kp 2
            65361: "left",      # kp 4
            65363: "right",     # kp 6
            65360: "leftup",    # kp 7
            65365: "rightup",   # kp 9
            65367: "leftdown",  # kp 1
            65366: "rightdown"  # kp 3
        }
    
        joystick_keys_windows_keycode = {
            96: "fire",       # kp 0 (numlock)
            104: "up",        # kp 8 (numlock)
            98: "down",       # kp 2 (numlock)
            100: "left",      # kp 4 (numlock)
            102: "right",     # kp 6 (numlock)
            103: "leftup",    # kp 7 (numlock)
            105: "rightup",   # kp 9 (numlock)
            97: "leftdown",   # kp 1 (numlock)
            99: "rightdown"   # kp 3 (numlock)
        }
    
        def keyrelease(self, event):
            print(time.time(), "KEYRELEASE {char!r} keysym='{keysym}' keycode={keycode} keysym_num={keysym_num} state={state}".format(**vars(event))) # XXX
            if sys.platform == "darwin":
                # OSX numkeys are problematic, I try to solve this via raw keycode
                if event.keycode in self.joystick_keys_osx:
                    print("JOYSTICK switch OFF:", self.joystick_keys_osx[event.keycode])
                    return
            elif sys.platform == "win32":
                # Windows numkeys are also problematic, need to solve this via keysym_num OR via keycode.. (sigh)
                if event.keysym_num in self.joystick_keys_windows_keysym_num:
                    print("JOYSTICK switch OFF:", self.joystick_keys_windows_keysym_num[event.keysym_num])
                    return
                elif event.keycode in self.joystick_keys_windows_keycode:
                    print("JOYSTICK switch OFF:", self.joystick_keys_windows_keycode[event.keycode])
                    return
            # sane platforms (Linux for one) play nice and just use the friendly keysym name.
            elif event.keysym in self.joystick_keys_sane_platforms:
                print("JOYSTICK switch OFF:", self.joystick_keys_sane_platforms[event.keysym])
                return
    
        def keypress(self, event):
            print(time.time(), "KEYPRESS {char!r} keysym='{keysym}' keycode={keycode} keysym_num={keysym_num} state={state}".format(**vars(event)))  # XXX
            if sys.platform == "darwin":
                # OSX numkeys are problematic, I try to solve this via raw keycode
                if event.keycode in self.joystick_keys_osx:
                    print("JOYSTICK switch ON:", self.joystick_keys_osx[event.keycode])
                    return
            elif sys.platform == "win32":
                # Windows numkeys are also problematic, need to solve this via keysym_num OR via keycode.. (sigh)
                if event.keysym_num in self.joystick_keys_windows_keysym_num:
                    print("JOYSTICK switch ON:", self.joystick_keys_windows_keysym_num[event.keysym_num])
                    return
                elif event.keycode in self.joystick_keys_windows_keycode:
                    print("JOYSTICK switch ON:", self.joystick_keys_windows_keycode[event.keycode])
                    return
            # sane platforms (Linux for one) play nice and just use the friendly keysym name.
            elif event.keysym in self.joystick_keys_sane_platforms:
                print("JOYSTICK switch ON:", self.joystick_keys_sane_platforms[event.keysym])
                return
    
    
    w = NumpadmadnessWindow()
    w.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
