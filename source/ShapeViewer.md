---
title: ShapeViewer
date: 2020-05-07
---
Example Python program ShapeViewer.py
This program creates a PyQt GUI

## Modules

* from qgis.core import *
* from qgis.gui import *
* from qgis.utils import iface
* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import QApplication, QMainWindow, QFileDialog, QVBoxLayout
* from PyQt5.QtGui import *
* import sys
* import os
* from shapeviewer_gui import Ui_MainWindow

## Classes

* class ShapeViewer(QMainWindow, Ui_MainWindow):

## Methods

*   def __init__(self):
* def main(argv):

## Code

Example Python PyQt program :

    from qgis.core import *
    from qgis.gui import *
    from qgis.utils import iface
    
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import QApplication, QMainWindow, QFileDialog, QVBoxLayout
    from PyQt5.QtGui import *
    
    import sys
    import os
    # Import our GUI
    from shapeviewer_gui import Ui_MainWindow
    
    # Environment variable QGISHOME must be set to the install directory
    # before running the application
    qgis_prefix = os.getenv("QGISHOME")
    
    class ShapeViewer(QMainWindow, Ui_MainWindow):
    
      def __init__(self):
        QMainWindow.__init__(self)
    
        # Required by Qt4 to initialize the UI
        self.setupUi(self)
    
        # Set the title for the app
        self.setWindowTitle("ShapeViewer")
    
        # Create the map canvas
        self.canvas = QgsMapCanvas()
        self.canvas.show()
    
        self.canvas.setCanvasColor(Qt.white)
        self.canvas.enableAntiAliasing(True)
    
        # Lay our widgets out in the main window using a 
        # vertical box layout
        self.layout = QVBoxLayout(self.frame)
        self.layout.addWidget(self.canvas)
    
        # layout is set - open a layer
        # Add an OGR layer to the map
        filename, filetype = QFileDialog.getOpenFileName(self, 
          "Open Shapefile", ".", "Shapefiles (*.shp)")
        #fileInfo = QFileInfo(file)
    
        # Add the layer
        layer = QgsVectorLayer(filename, "test", "ogr")
        if not layer.isValid():
          return
    
        QgsProject.instance().addMapLayer(layer)
        self.canvas.setExtent(layer.extent())
        self.canvas.setLayers([layer])
        layer.refresh()
        self.canvas.show()
        
    def main(argv):
      # create Qt application
      app = QApplication(argv)
    
      # Initialize qgis libraries
      QgsApplication.setPrefixPath(qgis_prefix, True)
      QgsApplication.initQgis()
    
      # create main window
      wnd = ShapeViewer()
      # Move the app window to upper left
      wnd.move(100,100)
      wnd.show()
    
      # run!
      retval = app.exec_()
      
      # exit
      QgsApplication.exitQgis()
      sys.exit(retval)
    
    
    if __name__ == "__main__":
      main(sys.argv)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
