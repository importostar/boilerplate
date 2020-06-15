---
title: oit
date: 2020-05-07
---
Example Python program oit.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import QTimer
* from PyQt5.QtWidgets import (QApplication, QMainWindow, QOpenGLWidget,
* from OpenGL import GLU, GL
* import numpy as np

## Classes

* class GLWidget(QOpenGLWidget):
* class MainWindow(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def initializeGL(self):
* def resizeGL(self, width, height):
* def paintGL(self):
* def initGeometry(self):
* def spin(self):
* def __init__(self):
* def initActions(self):
* def initMenus(self):
* def wire(self):
* def solid(self):
* def transparent(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtCore import QTimer
    from PyQt5.QtWidgets import (QApplication, QMainWindow, QOpenGLWidget,
                                 QAction, QActionGroup, QFileDialog)
    from OpenGL import GLU, GL
    import numpy as np
    
    
    class GLWidget(QOpenGLWidget):
        def __init__(self, parent=None):
            self.parent = parent
            super().__init__(parent)
            
            self.yRotDeg = 0.0       
            self.render_flag = 0
            self.initGeometry()
    
        def initializeGL(self):
            GL.glClearColor(1., 1., 1., 1.)
            GL.glEnable(GL.GL_DEPTH_TEST)
            GL.glDisable(GL.GL_CULL_FACE)
            GL.glColorMaterial(GL.GL_FRONT, GL.GL_AMBIENT_AND_DIFFUSE)
            GL.glEnable(GL.GL_COLOR_MATERIAL)
            GL.glShadeModel(GL.GL_SMOOTH)
    
            ambient = [0.0, 0.0, 0.0, 1.0]
            diffuse = [1.0, 1.0, 1.0, 1.0]
            specular = [1.0, 1.0, 1.0, 1.0]
    
            light_dir = [1.0, 0.0, 0.0, 0.0]
    
            GL.glLightfv(GL.GL_LIGHT0, GL.GL_AMBIENT, ambient)
            GL.glLightfv(GL.GL_LIGHT0, GL.GL_DIFFUSE, diffuse)
            GL.glLightfv(GL.GL_LIGHT0, GL.GL_SPECULAR, specular)
            GL.glLightfv(GL.GL_LIGHT0, GL.GL_POSITION, light_dir)
    
            GL.glEnable(GL.GL_LIGHT0)
            GL.glEnable(GL.GL_LIGHTING)
    
        def resizeGL(self, width, height):
            if height == 0:
                height = 1
    
            GL.glViewport(0, 0, width, height)
            GL.glMatrixMode(GL.GL_PROJECTION)
            GL.glLoadIdentity()
            aspect = width / float(height)
    
            GLU.gluPerspective(45.0, aspect, 1.0, 500.0)
            GL.glMatrixMode(GL.GL_MODELVIEW)
    
        def paintGL(self):
            GL.glClear(GL.GL_COLOR_BUFFER_BIT | GL.GL_DEPTH_BUFFER_BIT)
            GL.glLoadIdentity()
            GLU.gluLookAt(0.0, 130.0, 100.0, 0.0, 1.0, 0.0, 0.0, 0.0, 1.0)       
            GL.glRotate(self.yRotDeg, 0.0, 0.0, 1.0)
    
            GL.glColor4f(0.42, 0.42, 0.83, 1.0)
            #GL.glColor4f(0.0, 0.0, 1.0, 1.0)
            
            if self.render_flag == 0:
                GL.glPolygonMode(GL.GL_FRONT_AND_BACK, GL.GL_FILL)
            elif self.render_flag == 1:
                GL.glPolygonMode(GL.GL_FRONT_AND_BACK, GL.GL_LINE)
            else:
                GL.glDepthMask(GL.GL_FALSE)
                GL.glEnable(GL.GL_BLEND)
                GL.glBlendFunc(GL.GL_ZERO, GL.GL_ONE_MINUS_SRC_COLOR)
    
            GL.glEnableClientState(GL.GL_VERTEX_ARRAY)
            GL.glVertexPointerf(self.vertices)
            GL.glEnableClientState(GL.GL_NORMAL_ARRAY)
            GL.glNormalPointerf(self.normals)
            GL.glDrawElementsui(GL.GL_TRIANGLES, self.indices)
    
            GL.glPolygonMode(GL.GL_FRONT_AND_BACK, GL.GL_FILL)
            GL.glDepthMask(GL.GL_TRUE)
            GL.glDisable(GL.GL_BLEND)
    
        def initGeometry(self):
            self.vertices = np.loadtxt('vertices.txt', dtype=np.float32)
            self.indices = np.loadtxt('indices.txt', dtype=int)
            self.normals = np.loadtxt('normals.txt', dtype=np.float32)
    
        def spin(self):
            self.yRotDeg = (self.yRotDeg + 1) % 360.0
            self.parent.statusBar().showMessage('rotation {}'.format(self.yRotDeg))
            self.update()
    
    class MainWindow(QMainWindow):
    
        def __init__(self):
            super().__init__()
    
            self.resize(500, 500)
            self.setWindowTitle('Order Independent Transparency')
    
            self.initActions()
            self.initMenus()
    
            self.glWidget = GLWidget(self)
            self.setCentralWidget(self.glWidget)
    
            timer = QTimer(self)
            timer.setInterval(20)
            timer.timeout.connect(self.glWidget.spin)
            timer.start()
    
        def initActions(self):
            self.exitAction = QAction('Quit', self)
            self.exitAction.setShortcut('Ctrl+Q')
            self.exitAction.setStatusTip('Exit application')
            self.exitAction.triggered.connect(self.close)
    
            self.solidAction = QAction('Show Solid', self)
            self.solidAction.setStatusTip('Show Solid')
            self.solidAction.setCheckable(True)
            self.solidAction.setChecked(True)
            self.solidAction.triggered.connect(self.solid)
    
            self.wireAction = QAction('Show Wireframe', self)
            self.wireAction.setStatusTip('Show Wireframe')
            self.wireAction.setCheckable(True)
            self.wireAction.triggered.connect(self.wire)
    
            self.transparentAction = QAction('Show Transparent', self)
            self.transparentAction.setStatusTip('Show Transparent')
            self.transparentAction.setCheckable(True)
            self.transparentAction.triggered.connect(self.transparent)
    
            action_group = QActionGroup(self)
            action_group.addAction(self.solidAction)
            action_group.addAction(self.wireAction)
            action_group.addAction(self.transparentAction)
    
    
        def initMenus(self):
            menuBar = self.menuBar()
            fileMenu = menuBar.addMenu('&File')
            fileMenu.addAction(self.exitAction)
    
            viewMenu = menuBar.addMenu('View')
            viewMenu.addAction(self.solidAction)
            viewMenu.addAction(self.wireAction)
            viewMenu.addAction(self.transparentAction)
    
        def wire(self):
            self.glWidget.render_flag = 1
        
        def solid(self):
            self.glWidget.render_flag = 0
        
        def transparent(self):
            self.glWidget.render_flag = 2
    
    app = QApplication(sys.argv)
    
    win = MainWindow()
    win.show()
    
    sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
