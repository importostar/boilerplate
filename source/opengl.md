---
title: opengl
date: 2020-05-07
---
Example Python program opengl.py

## Modules

* from PyQt5.QtCore import QUrl, qDebug, QObject
* from PyQt5.QtGui import QGuiApplication, QOpenGLFramebufferObjectFormat, QOpenGLFramebufferObject
* from PyQt5.QtQml import qmlRegisterType
* from PyQt5.QtQuick import QQuickItem, QQuickView, QQuickFramebufferObject
* import sys

## Classes

* class FbItemRenderer(QQuickFramebufferObject.Renderer):
* class FBORenderItem(QQuickFramebufferObject):

## Methods

* def __init__(self, parent=None):
* def createFrameBufferObject(self, size):
* def synchronize(self, item):
* def render(self):
* def __init__(self, parent=None):
* def createRenderer(self):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import QUrl, qDebug, QObject
    from PyQt5.QtGui import QGuiApplication, QOpenGLFramebufferObjectFormat, QOpenGLFramebufferObject
    from PyQt5.QtQml import qmlRegisterType
    from PyQt5.QtQuick import QQuickItem, QQuickView, QQuickFramebufferObject
    
    
    class FbItemRenderer(QQuickFramebufferObject.Renderer):
        def __init__(self, parent=None):
            super(FbItemRenderer, self).__init__()
            qDebug("Creating FbItemRenderer")
    
        def createFrameBufferObject(self, size):
            qDebug("Creating FrameBufferObject")
            format = QOpenGLFramebufferObjectFormat()
            format.setAttachment(QOpenGLFramebufferObject.Depth)
            return QOpenGLFramebufferObject(size, format)
    
        def synchronize(self, item):
            qDebug("Synchronizing")
    
        def render(self):
            qDebug("Render")
            # Called with the FBO bound and the viewport set.
            # ... Issue OpenGL commands.
    
    
    class FBORenderItem(QQuickFramebufferObject):
        def __init__(self, parent=None):
            qDebug("Create fborenderitem")
            super(FBORenderItem, self).__init__(parent)
    
        def createRenderer(self):
            qDebug("Create renderer")
            return FbItemRenderer()
    
    
    if __name__ == '__main__':
        import sys
    
        app = QGuiApplication(sys.argv)
    
        qmlRegisterType(FBORenderItem, "Renderer", 1, 0, "FBORenderer")
    
        view = QQuickView()
        view.setSource(QUrl("main.qml"))
        view.show()
    
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
