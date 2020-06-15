---
title: test_pygame (1)
date: 2020-05-07
---
Example Python program test_pygame (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import pygame
* import numpy as np
* import time

## Code

Python example

    #!/usr/bin/env python
    #coding=utf-8
    
    # Sample Python/Pygame Programs
    # Simpson College Computer Science
    # http://cs.simpson.edu
    import pygame
    # Define some colors
    black = ( 0, 0, 0)
    white = ( 255, 255, 255)
    green = ( 0, 255, 0)
    red = ( 255, 0, 0)
    pygame.init()
    # Set the height and width of the screen
    size=[700,500]
    screen=pygame.display.set_mode(size)
    pygame.display.set_caption("My Game")
    #Loop until the user clicks the close button.
    done=False
    # Used to manage how fast the screen updates
    clock=pygame.time.Clock()
    
    import numpy as np
    import time
    
    # -------- Main Program Loop -----------
    while done==False:
        for event in pygame.event.get(): # User did something
            if event.type == pygame.QUIT: # If user clicked close
                done=True # Flag that we are done so we exit this loop
        # Set the screen background
        screen.fill(black)
        # ALL CODE TO DRAW SHOULD GO BELOW THIS COMMENT
        segs = np.random.rand(30, 50000, 2)*np.array(size)[None, None, :]
        start = time.time()
        for i in xrange(segs.shape[1]):
            pygame.draw.lines(screen,green, False, segs[:,i,:],1)
        # ALL CODE TO DRAW SHOULD GO ABOVE THIS COMMENT
        # Limit to 20 frames per second
        clock.tick(20)
        # Go ahead and update the screen with what we've drawn.
        pygame.display.flip()
        print "It took:", time.time()-start, 's'
        # Be IDLE friendly. If you forget this line, the program will 'hang'
        # on exit.
    pygame.quit ()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
