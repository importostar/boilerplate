---
title: Certipy (1)
date: 2020-05-07
---
Example Python program Certipy (1).py

## Modules

* import cvs
* from PIL import Image
* from PIL import ImageFont
* from PIL import ImageDraw
* import pygame
* from main.py import *

## Methods

* def center_xy(text,xy):
* def rungeneration(temp_path):
* def generateCerts():

## Code

Python example

    import cvs
    from PIL import Image
    from PIL import ImageFont
    from PIL import ImageDraw
    import pygame
    from main.py import *
    
    def center_xy(text,xy):
        fsize_x, fsize_y = PIL_draw.textsize(text, font)
        x = int(xy[0]float((fsize_x)/2))
    
    def rungeneration(temp_path):
    
    draw_start = False
    to_draw = []
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
    
            if event.type == pygame.MOUSEMOTION:
    			mouse_pos = mouse_x, mouse_y = pygame.mouse.get_pos()
    
            if event.type == pygame.MOUSEBUTTONDOWN:
    			pos = mouse_pos
    			draw_start = True
    
    
    		if event.type == pygame.MOUSEBUTTONUP:
    			final_pos = mouse_pos
    			draw_start = False
    			rect = pygame.Rect(pos,(final_pos[0]- pos[0], final_pos[1]-pos[1]))
    			rect.normalize()
    			to_draw+=[rect]
    
            if event.type == pygame.KEYDOWN:
    			if event.key == pygame.K_ESCAPE:
    				running = False
    
            if event.key == pygame.K_RETURN:
    
    				print to_draw[0]
    
    				generate_output(to_draw)
    
    
    
    			if event.key == pygame.K_BACKSPACE:
    				to_draw.pop()
    
    
    #setresolution of photo or get resolution of photo
    
    #first is to set the resolution of the dialogpage
    #match the resolution of dialog page to photo
    def generateCerts():
    
    clock.tick(30)
    	pygame.display.update()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
