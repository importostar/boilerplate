---
title: chat_summit_feiji_bullet
date: 2020-05-07
---
Example Python program chat_summit_feiji_bullet.py

## Modules

* from __future__ import unicode_literals
* import pygame

## Classes

* class Bullet1(pygame.sprite.Sprite):
* class Bullet2(pygame.sprite.Sprite):

## Methods

* def __init__(self, position):
* def move(self):
* def reset(self, position):
* def __init__(self, position):
* def move(self):
* def reset(self, position):

## Code

Python example

    # -*- coding: utf-8 -*-
    from __future__ import unicode_literals
    import pygame
    
    
    class Bullet1(pygame.sprite.Sprite):
    
        def __init__(self, position):
            pygame.sprite.Sprite.__init__(self)
    
            self.image = pygame.image.load("images/bullet1.png").convert_alpha()
            self.rect = self.image.get_rect()
            self.rect.left, self.rect.top = position
            self.speed = 25
            self.active = False
            self.mask = pygame.mask.from_surface(self.image)
    
        def move(self):
            self.rect.top -= self.speed
    
            if self.rect.top < 0:
                self.active = False
    
        def reset(self, position):
            self.rect.left, self.rect.top = position
            self.active = True
    
    
    class Bullet2(pygame.sprite.Sprite):
    
        def __init__(self, position):
            pygame.sprite.Sprite.__init__(self)
    
            self.image = pygame.image.load("images/bullet2.png").convert_alpha()
            self.rect = self.image.get_rect()
            self.rect.left, self.rect.top = position
            self.speed = 20
            self.active = False
            self.mask = pygame.mask.from_surface(self.image)
    
        def move(self):
            self.rect.top -= self.speed
    
            if self.rect.top < 0:
                self.active = False
    
        def reset(self, position):
            self.rect.left, self.rect.top = position
            self.active = True
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/