---
title: pygamemp3player
date: 2020-05-07
---
Example Python program pygamemp3player.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pygame
* import time
* import pynput
* from tkinter import *  # not advisable to import everything with *
* from tkinter import filedialog

## Code

Python tkinter example

    import pygame
    import time
    import pynput
    mouse = pynput.mouse.Controller()
    
    pygame.init()
    font=pygame.font.Font('freesansbold.ttf',32)
    screen2=pygame.display.set_mode((1280,720))
    screen=pygame.Surface((800,600))
    screen.fill((90,90,40))
    sec=font.render("-- Başlat",True,(255,255,255))
    diger=font.render("Durdur",True,(255,255,255))
    dosyasec=font.render("Dosya Seç",True,(255,255,255))
    screen.blit(sec,(50,50))
    screen.blit(diger,(50,100))
    screen.blit(dosyasec,(50,150))
    running=True
    start=False
    
    from tkinter import *  # not advisable to import everything with *
    from tkinter import filedialog
    #root=Tk()
        
    pygame.mixer.init()
    #pygame.mixer.music.load("C:\\Users\\user2\\Music\\onira.mp3")
    #audio_file_name = filedialog.askopenfilename(filetypes=(("Audio Files", ".wav .ogg",".mp3"),   ("All Files", "*.*")))
    #print(audio_file_name)
    while running:
        screen2.blit(screen,(100,100))
        pygame.display.update()
        
        for event in pygame.event.get():
            #print(event.type)
            if event.type==pygame.QUIT:
                running=False
        if pygame.mouse.get_pressed()[0]:
               coords = pygame.mouse.get_pos()
               if coords[0]>1205 and coords[1]==0:
                   running=False
               if coords[0]>=150 and coords[0]<=304 and coords[1]>150 and coords[1]<185 : #PLay button
                 
                  if not start:
                     try: 
                        pygame.mixer.music.play()
                        start=True
                     except:
                         pass   
                  else:
                      pygame.mixer.music.unpause()   
               elif coords[0]>=150 and coords[0]<=235 and coords[1]>206 and coords[1]<236 :
                     pygame.mixer.music.pause()
                     start=False   
               elif coords[0]>=150 and coords[0]<=314 and coords[1]>250 and coords[1]<280:
                    coords==None
                    #root=Tk()
                    if not start:
                       root=Tk() 
                       audio_file_name = filedialog.askopenfilename(filetypes=(("Audio Files", ".wav .ogg",".mp3"),   ("All Files", "*.*")))
                       start=True
                       root.quit()
                       root.destroy()
                       #Tkinter kapandıktan sonra sol click basılı kalıyor. 
                       mouse.click(pynput.mouse.Button.left, 1) #1 Sol klik simülasyonu ile takılı kalmasını yok edebilirsiniz. 
                    pygame.mixer.music.load(audio_file_name)
                    
                    pygame.mixer.music.play()
                    
    
    
         
               #print(coords)        
    # Evet bu şekilde tek tek tuşlar için yazmak gerekiyor her şeyi.           

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
