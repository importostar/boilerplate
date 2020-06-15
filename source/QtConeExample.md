---
title: QtConeExample
date: 2020-05-07
---
Example Python program QtConeExample.py
This program creates a PyQt GUI

## Modules

* import sys
* from vtk import vtkActor
* from vtk import vtkConeSource
* from vtk import vtkPolyDataMapper
* from vtk import vtkRenderer
* from PySide2.QtCore import Qt
* from PySide2.QtWidgets import QApplication
* from QVTKRenderWindowInteractor import QVTKRenderWindowInteractor

## Methods

* def QVTKRenderWidgetConeExample(argv):

## Code

Python example

    # coding=utf-8
    
    import sys
    
    from vtk import vtkActor
    from vtk import vtkConeSource
    from vtk import vtkPolyDataMapper
    from vtk import vtkRenderer
    from PySide2.QtCore import Qt
    from PySide2.QtWidgets import QApplication
    from QVTKRenderWindowInteractor import QVTKRenderWindowInteractor
    
    def QVTKRenderWidgetConeExample(argv):
        """A simple example that uses the QVTKRenderWindowInteractor class."""
    
        # every QT app needs an app
        app = QApplication(['QVTKRenderWindowInteractor'])
    
        # create the widget
        widget = QVTKRenderWindowInteractor()
        widget.Initialize()
        widget.Start()
    
        # if you don't want the 'q' key to exit, comment this out
        widget.AddObserver("ExitEvent", lambda o, e, a=app: a.quit())
    
        ren = vtkRenderer()
        widget.GetRenderWindow().AddRenderer(ren)
    
        cone = vtkConeSource()
        cone.SetResolution(8)
    
        coneMapper = vtkPolyDataMapper()
        coneMapper.SetInputConnection(cone.GetOutputPort())
    
        coneActor = vtkActor()
        coneActor.SetMapper(coneMapper)
    
        ren.AddActor(coneActor)
    
        # show the widget
        widget.show()
        # start event processing
        app.exec_()
    
    if __name__ == "__main__":
        QVTKRenderWidgetConeExample(sys.argv)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
