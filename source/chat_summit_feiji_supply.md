---
title: chat_summit_feiji_supply
date: 2020-05-07
---
Example Python program chat_summit_feiji_supply.py

## Modules

* import pygame
* from random import *

## Classes

* class Bullet_Supply(pygame.sprite.Sprite):
* class Bomb_Supply(pygame.sprite.Sprite):

## Methods

* def __init__(self, bg_size):
* def move(self):
* def reset(self):
* def __init__(self, bg_size):
* def move(self):
* def reset(self):

## Code

Python example

    import pygame
    from random import *
    
    class Bullet_Supply(pygame.sprite.Sprite):
        def __init__(self, bg_size):
            pygame.sprite.Sprite.__init__(self)
    
            self.image = pygame.image.load("images/bullet_supply.png").convert_alpha()
            self.rect = self.image.get_rect()
            self.width, self.height = bg_size[0], bg_size[1]
            self.rect.left, self.rect.bottom = \
                            randint(0, self.width - self.rect.width), -100
            self.speed = 5
            self.active = False
            self.mask = pygame.mask.from_surface(self.image)
    
        def move(self):
            if self.rect.top < self.height:
                self.rect.top += self.speed
            else:
                self.active = False
    
        def reset(self):
            self.active = True
            self.rect.left, self.rect.bottom = \
                            randint(0, self.width - self.rect.width), -100
                     
    class Bomb_Supply(pygame.sprite.Sprite):
        def __init__(self, bg_size):
            pygame.sprite.Sprite.__init__(self)
    
            self.image = pygame.image.load("images/bomb_supply.png").convert_alpha()
            self.rect = self.image.get_rect()
            self.width, self.height = bg_size[0], bg_size[1]
            self.rect.left, self.rect.bottom = \
                            randint(0, self.width - self.rect.width), -100
            self.speed = 5
            self.active = False
            self.mask = pygame.mask.from_surface(self.image)
    
        def move(self):
            if self.rect.top < self.height:
                self.rect.top += self.speed
            else:
                self.active = False
    
        def reset(self):
            self.active = True
            self.rect.left, self.rect.bottom = \
                            randint(0, self.width - self.rect.width), -100                                          
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
