---
title: customizer
date: 2020-05-07
---
Example Python program customizer.py

## Modules

* import pyz3r
* import tkinter as tk
* import sys
* from tkinter.filedialog import askopenfilename, asksaveasfilename
* from tkinter import messagebox
* from tkinter import simpledialog
* import traceback

## Methods

* def show_exception_and_exit(exc_type, exc_value, tb):
* def main():
* def read_rom(srcfilepath):
* def ask_heartspeed():
* def ask_heartcolor():
* def ask_sprite():
* def ask_music():

## Code

Python tkinter example

    import pyz3r
    import tkinter as tk
    import sys
    from tkinter.filedialog import askopenfilename, asksaveasfilename
    from tkinter import messagebox
    from tkinter import simpledialog
    
    def show_exception_and_exit(exc_type, exc_value, tb):
        import traceback
        traceback.print_exception(exc_type, exc_value, tb)
        input("Press key to exit.")
        sys.exit(-1)
    
    sys.excepthook = show_exception_and_exit
    
    game = pyz3r.alttpr(randomizer='entrance')
    
    def main():
    
        srcfilename = askopenfilename(
                filetypes =(("SFC", "*.sfc"),("all files","*.*")),
                title = "Find a v30 ALTTPR ROM to patch."
            )
        
        patchrom_array = read_rom(srcfilename)
    
        #apply the heart speed change
        patchrom_array = game.patch(
            rom=patchrom_array,
            patches=game.get_patch_heart_speed(ask_heartspeed())
        )
    
        #apply the heart color change
        patchrom_array = game.patch(
            rom=patchrom_array,
            patches=game.get_patch_heart_color(ask_heartcolor())
        )
    
        #apply the sprite
        patchrom_array = game.patch(
            rom=patchrom_array,
            patches=game.get_patch_sprite(name=ask_sprite())
        )
    
        #apply the sprite
        patchrom_array = game.patch(
            rom=patchrom_array,
            patches=game.get_patch_music(music=ask_music())
        )
    
        #calculate the SNES checksum and apply it to the ROM
        patchrom_array = game.patch(
            rom=patchrom_array,
            patches=game.checksum_patch(patchrom_array)
        )
    
        dstfilename = asksaveasfilename(
                filetypes =(("SFC", "*.sfc"),("all files","*.*")),
                title = "Save customized ROM"
            )
    
        game.write_rom(patchrom_array, dstfilename)
    
    
    def read_rom(srcfilepath):
        fr = open(srcfilepath,"rb")
        baserom_array = list(fr.read())
        fr.close()
        return baserom_array
    
    def ask_heartspeed():
        MsgBox = simpledialog.askstring('Heart Beep Speed','Beep speed? (off, quarter, half, full, double)  Leave blank for quarter.')
        return MsgBox
    
    def ask_heartcolor():
        MsgBox = simpledialog.askstring('Heart Color','Heart color? (red, blue, green, yellow). Leave blank for red.')
        return MsgBox
    
    def ask_sprite():
        MsgBox = simpledialog.askstring('Sprite Selection','Name of sprite (as listed on https://alttpr.com/en/sprite_preview).  Leave blank for Link.')
        return MsgBox
    
    def ask_music():
        MsgBox = messagebox.askquestion('Music','Do you want in-game music?')
        if MsgBox == 'yes':
            return True
        else:
            return False
    
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
