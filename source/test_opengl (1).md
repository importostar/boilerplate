---
title: test_opengl (1)
date: 2020-05-07
---
Example Python program test_opengl (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from OpenGL.GL import *
* from OpenGL.GLUT import *
* from OpenGL.GLU import *
* import sys
* import time
* import numpy as np

## Methods

* def InitGL(Width, Height):				# We call this right after our OpenGL window is created.
* def ReSizeGLScene(Width, Height):
* def DrawGLScene():
* def keyPressed(*args):
* def main():

## Code

Python example

    #!/usr/bin/env python
    from OpenGL.GL import *
    from OpenGL.GLUT import *
    from OpenGL.GLU import *
    OpenGL.ERROR_ON_COPY = True
    import sys
    # Some api in the chain is translating the keystrokes to this octal string
    # so instead of saying: ESCAPE = 27, we use the following.
    ESCAPE = '\033'
    
    # Number of the glut window.
    window = 0
    
    # A general OpenGL initialization function.  Sets all of the initial parameters. 
    def InitGL(Width, Height):				# We call this right after our OpenGL window is created.
        glClearColor(0.0, 0.0, 0.0, 0.0)	# This Will Clear The Background Color To Black
        glClearDepth(1.0)					# Enables Clearing Of The Depth Buffer
        glDepthFunc(GL_LESS)				# The Type Of Depth Test To Do
        glEnable(GL_DEPTH_TEST)				# Enables Depth Testing
        glShadeModel(GL_SMOOTH)				# Enables Smooth Color Shading
    	
        glMatrixMode(GL_PROJECTION)
        glLoadIdentity()					# Reset The Projection Matrix
    										# Calculate The Aspect Ratio Of The Window
        gluPerspective(45.0, float(Width)/float(Height), 0.1, 100.0)
    
        glMatrixMode(GL_MODELVIEW)
    
    # The function called when our window is resized (which shouldn't happen if you enable fullscreen, below)
    def ReSizeGLScene(Width, Height):
        if Height == 0:						# Prevent A Divide By Zero If The Window Is Too Small 
    	    Height = 1
    
        glViewport(0, 0, Width, Height)		# Reset The Current Viewport And Perspective Transformation
        glMatrixMode(GL_PROJECTION)
        glLoadIdentity()
        gluPerspective(45.0, float(Width)/float(Height), 0.1, 100.0)
        glMatrixMode(GL_MODELVIEW)
    
    # The main drawing function. 
    def DrawGLScene():
        # Clear The Screen And The Depth Buffer
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
        glLoadIdentity()					# Reset The View 
    
        # Move Left 1.5 units and into the screen 6.0 units.
        glTranslatef(0, 0.0, -4.0)
        # Draw a triangle
        import time
        import numpy as np
        n_pts = 34
        n_spikes =50000
        t = np.linspace(-2, 2, n_pts)
        y= 1.5*(2*np.random.rand(n_pts,n_spikes)-1)
        start = time.time()
        vertices = np.empty((n_spikes, n_pts, 2), dtype=np.float)
        vertices[:,:,0] = t[:, None].T
        vertices[:,:,1] = y.T
        vertices = vertices.reshape(-1, 2)
        glEnableClientState(GL_VERTEX_ARRAY)
        glVertexPointer(2, GL_FLOAT, 0, vertices)
        for i in xrange(n_spikes):
            glDrawArrays(GL_LINE_STRIP, i*n_pts, n_pts)     
        glDisableClientState(GL_VERTEX_ARRAY);
        
        #  since this is double buffered, swap the buffers to display what just got drawn. 
        glutSwapBuffers()
        print "It took:", time.time()-start, 's'
    
    # The function called whenever a key is pressed. Note the use of Python tuples to pass in: (key, x, y)  
    def keyPressed(*args):
    	# If escape is pressed, kill everything.
        if args[0] == ESCAPE:
    	    glutDestroyWindow(window)
    	    sys.exit()
    
    def main():
    	global window
    	# For now we just pass glutInit one empty argument. I wasn't sure what should or could be passed in (tuple, list, ...)
    	# Once I find out the right stuff based on reading the PyOpenGL source, I'll address this.
    	glutInit(())
    
    	# Select type of Display mode:   
    	#  Double buffer 
    	#  RGBA color
    	# Alpha components supported 
    	# Depth buffer
    	glutInitDisplayMode(GLUT_RGBA | GLUT_DOUBLE | GLUT_ALPHA | GLUT_DEPTH)
    	
    	# get a 640 x 480 window 
    	glutInitWindowSize(800, 600)
    	
    	# the window starts at the upper left corner of the screen 
    	glutInitWindowPosition(0, 0)
    	
    	# Okay, like the C version we retain the window id to use when closing, but for those of you new
    	# to Python (like myself), remember this assignment would make the variable local and not global
    	# if it weren't for the global declaration at the start of main.
    	window = glutCreateWindow("Jeff Molofee's GL Code Tutorial ... NeHe '99")
    
       	# Register the drawing function with glut, BUT in Python land, at least using PyOpenGL, we need to
    	# set the function pointer and invoke a function to actually register the callback, otherwise it
    	# would be very much like the C version of the code.	
    	glutDisplayFunc (DrawGLScene)
    	
    	# Uncomment this line to get full screen.
    	#glutFullScreen()
    
    	# When we are doing nothing, redraw the scene.
    	glutIdleFunc(DrawGLScene)
    	
    	# Register the function called when our window is resized.
    	glutReshapeFunc (ReSizeGLScene)
    	
    	# Register the function called when the keyboard is pressed.  
    	glutKeyboardFunc (keyPressed)
    
    	# Initialize our window. 
    	InitGL(800, 600)
    
    	# Start Event Processing Engine	
    	glutMainLoop()
    
    # Print message to console, and kick off the main to get it rolling.
    print "Hit ESC key to quit."
    main()
        	
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
