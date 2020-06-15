---
title: pycrystal
date: 2020-05-07
---
Example Python program pycrystal.py

## Modules

* import pygame
* import random

## Methods

* def init(array, parts):
* def move(array, parts, position):
* def crystalize(array, parts):
* def main():

## Code

Python example

    import pygame
    import random
    
    CRYSTAL = 0
    PARTICLE = 192<<16 | 192<<8 | 192
    EMPTY = 16777215
    
    def init(array, parts):
      for y in xrange(20, 480, 2):
        for x in xrange(20, 480, 2):
          array[x][y] = PARTICLE
          parts[(x, y)] = PARTICLE
    
      array[0][250] = CRYSTAL
      parts[(0, 250)] = CRYSTAL
    
    
    def move(array, parts, position):
      x, y = position
      u = random.randint(-1, 1)
      v = random.randint(-1, 1)
      xx = x + u
      yy = y + v
    
      if xx > 499:
        xx = 0
    
      elif xx < 0:
        xx = 499
    
      if yy > 499:
        yy = 0
    
      elif yy < 0:
        yy = 499
    
      if parts.has_key((xx, yy)):
        dest = parts[(xx, yy)]
        if dest == 0:
          array[x][y] = CRYSTAL
          parts[(x, y)] = CRYSTAL
    
      else:
        array[x][y] = EMPTY
        del parts[(x, y)]
    
        array[xx][yy] = PARTICLE
        parts[(xx, yy)] = PARTICLE
    
    
    def crystalize(array, parts):
      for position, value in parts.items():
        if value == PARTICLE:
          move(array, parts, position)
    
    
    def main():
      pygame.display.init()
      surf = pygame.display.set_mode((500, 500))
      surf.fill((255, 255, 255))
      array = pygame.surfarray.pixels2d(surf)
      parts = {}
    
      init(array, parts)
    
      while pygame.event.poll().type != pygame.KEYDOWN:
        crystalize(array, parts)
        pygame.display.update()
    
      pygame.display.quit()
    
    
    if __name__ == '__main__':
      main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
