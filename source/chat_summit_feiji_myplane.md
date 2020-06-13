---
title: chat_summit_feiji_myplane
date: 2020-05-07
---
Example Python program chat_summit_feiji_myplane.py

## Modules

* from __future__ import unicode_literals
* import pygame

## Classes

* class MyPlane(pygame.sprite.Sprite):

## Methods

* def __init__(self, bg_size):
* def moveUp(self):
* def moveDown(self):
* def moveLeft(self):
* def moveRight(self):
* def reset(self):

## Code

Python example

    # -*- coding: utf-8 -*-
    from __future__ import unicode_literals
    import pygame
    
    
    class MyPlane(pygame.sprite.Sprite):
    
        def __init__(self, bg_size):
            pygame.sprite.Sprite.__init__(self)
            self.image = pygame.image.load("images/me1.png").convert_alpha()
            self.image1 = pygame.image.load("images/me2.png").convert_alpha()
            self.destroy_images = []
            self.destroy_images.extend([
                pygame.image.load("images/me_destroy_1.png").convert_alpha(),
                pygame.image.load("images/me_destroy_2.png").convert_alpha(),
                pygame.image.load("images/me_destroy_3.png").convert_alpha(),
                pygame.image.load("images/me_destroy_4.png").convert_alpha(),
                pygame.image.load("images/me_destroy_5.png").convert_alpha()
            ])
    
            self.rect = self.image.get_rect()
            self.width, self.height = bg_size[0], bg_size[1]
            self.rect.left, self.rect.top = \
                (self.width - self.rect.width) // 2, \
                self.height - self.rect.height - 60
            self.speed = 10
            self.active = True
            self.invincible = False
            self.mask = pygame.mask.from_surface(self.image1)
    
        def moveUp(self):
            if self.rect.top > 0:
                self.rect.top -= self.speed
            else:
                self.rect.top = 0
    
        def moveDown(self):
            if self.rect.bottom < self.height - 60:
                self.rect.top += self.speed
            else:
                self.rect.bottom = self.height - 60
    
        def moveLeft(self):
            if self.rect.left > 0:
                self.rect.left -= self.speed
            else:
                self.rect.left = 0
    
        def moveRight(self):
            if self.rect.right < self.width:
                self.rect.left += self.speed
            else:
                self.rect.right = self.width
    
        def reset(self):
            self.rect.left, self.rect.top = \
                (self.width - self.rect.width) // 2, \
                self.height - self.rect.height - 60
            self.active = True
            self.invincible = True
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
