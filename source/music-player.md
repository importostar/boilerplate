---
title: music player
date: 2020-05-07
---
Example Python program music-player.py

## Modules

* import os
* import pygame
* import tkinter
* from mutagen.id3 import ID3

## Methods

* def loadandplaysong():  # wrap load and play current song logic into new function
* def nextsong(event):
* def previoussong(event):
* def stopsong(event):
* def resumesong(event):
* def updatelabel():
* def checksongend():  # new function to check if current song is ended

## Code

Python tkinter example

    import os
    import pygame
    import tkinter
    from mutagen.id3 import ID3
    
    music_dir = '[path]'  # move music folder path to here
    
    root = tkinter.Tk()
    root.minsize(300, 300)
    listofsongs = []
    realnames = []
    index = 0
    v = tkinter.StringVar()
    
    
    def loadandplaysong():  # wrap load and play current song logic into new function
        pygame.mixer.music.load(listofsongs[index])
        pygame.mixer.music.play()
        updatelabel()
    
    
    def nextsong(event):
        global index
        if index < len(listofsongs) - 1:
            index += 1
        else:
            index = 0
        loadandplaysong()
    
    
    def previoussong(event):
        global index
        if index > 0:
            index -= 1
        else:
            index = len(listofsongs) - 1
        loadandplaysong()
    
    
    def stopsong(event):
        pygame.mixer.music.pause()
        updatelabel()
    
    
    def resumesong(event):
        pygame.mixer.music.unpause()
        updatelabel()
    
    
    def updatelabel():
        global index
        v.set(realnames[index])
    
    
    add = os.chdir(music_dir)
    for files in os.listdir(add):
        if files.endswith(('.mp3', '.flac')):  # One can use tuple in endswith function. Ref: https://stackoverflow.com/a/18351977
            realdir = os.path.realpath(files)
            audio = ID3(realdir)
            if 'TIT2' in audio:
                realnames.append(audio['TIT2'].text[0])
            else:  # For files that don't have TIT2 field
                realnames.append(files)
            listofsongs.append(files)
    
    
    pygame.init()
    pygame.mixer.init()
    loadandplaysong()
    SONG_END = pygame.USEREVENT  # SONG_END is corresponding to music playing logic, so move it to here.
    pygame.mixer.music.set_endevent(SONG_END)
    
    label = tkinter.Label(root, text="Music Player")
    label.pack()
    listbox = tkinter.Listbox(root)
    listbox.pack()
    
    for item in realnames:
        listbox.insert(tkinter.END, item)  # One can use this way to append to listbox end, reverse is not necessary.
    
    nextbutton = tkinter.Button(root, text='下一首')
    nextbutton.pack()
    
    previousbutton = tkinter.Button(root, text='上一首')
    previousbutton.pack()
    
    stopbutton = tkinter.Button(root, text='暫停')
    stopbutton.pack()
    
    resumebutton = tkinter.Button(root, text='繼續播放')
    resumebutton.pack()
    
    songlabel = tkinter.Label(root, textvariable=v, width=35)
    songlabel.pack()
    
    nextbutton.bind("<Button-1>", nextsong)
    previousbutton.bind("<Button-1>", previoussong)
    stopbutton.bind("<Button-1>", stopsong)
    resumebutton.bind("<Button-1>", resumesong)
    
    
    def checksongend():  # new function to check if current song is ended
        for event in pygame.event.get():
            if event.type == SONG_END:
                nextsong(event)
        root.after(0, checksongend)
    
    
    root.after(0, checksongend)  # One can use this to execute code (pygame event loop in your case) with tkinter main loop. Ref: https://stackoverflow.com/a/459131
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
