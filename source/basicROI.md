---
title: basicROI
date: 2020-05-07
---
Example Python program basicROI.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import QSize, QPoint, Qt
* from PyQt5.QtGui import (QBrush, QPainter, QPen, QPixmap, QColor)
* from PyQt5.QtWidgets import (QApplication, QVBoxLayout, QWidget)
* 	import sys

## Classes

* class Window(QWidget):

## Methods

* 	def __init__(self):
* 	def paintEvent(self, event):
* 	def mousePressEvent(self, event):
* 	def mouseReleaseEvent(self, event):
* 	def mouseMoveEvent(self, event):
* 	def closeEvent(self, event):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    	
    from PyQt5.QtCore import QSize, QPoint, Qt
    from PyQt5.QtGui import (QBrush, QPainter, QPen, QPixmap, QColor)
    from PyQt5.QtWidgets import (QApplication, QVBoxLayout, QWidget)
    
      
    class Window(QWidget):
    	def __init__(self):
    		super(Window, self).__init__()
      
    		# Creas un layout que será la base donde pintemos
    		mainLayout = QVBoxLayout()
    
    		# Desactivas el seguimiento del raton. Si lo activas nunca podrás tener un rectángulo fijo.
    		# Prueba a ponerlo a True para ver la diferencia.
    		self.setMouseTracking(False)
    
    		# Fijamos el tamaño minimo de la ventana.
    		self.setMinimumSize(QSize(640,480))	
    		# Asignamos el layout a la ventana
    		self.setLayout(mainLayout)
    
    		# Ponemos titulo a la ventana
    		self.setWindowTitle("Basic ROI")
    
    		# Creamos los puntos de inicio y final del ROI
    		self.startPoint = QPoint(-10,-10)
    		self.endPoint = QPoint(-10,-10)
    
    
    	# Esta función pintará lo que se le diga cada vez que se lance el evento PaintEvent
    	# La instruccion self.update() lanza este evento.
    	def paintEvent(self, event):
    
    		print("repainting")
    
    		# Creamos un painter que es el que sabe dibujar cosas
    		painter = QPainter(self)
    
    		# En lugar de utilizar un Qlabel donde poner la imagen, la pintamos directamente en la ventana. Es más eficiente.
    		# Si necesitas un QLabel, sí o sí, te tendrás que pelear con el orden de pintado de Qt. Juega a tu gusto.
    		painter.drawPixmap(0,0,640,480,QPixmap("./resources/mario.jpg"))
    
    		# Asignamos un estilo de lapiz (para pintar los bordes del ROI)
    		painter.setPen(QPen(QColor(Qt.gray), 1))
    		# Asignamos un estilo de pincel (para rellenar el ROI, RGBAlpha. El Alpha es el nivel de transparencia)
    		painter.setBrush(QBrush(QColor(255, 200, 200, 100)))
    
    		# Para que pinte el punto sólo cuando hayamos hecho click con el boton izquierdo del raton, ponemos esta condición.
    		# No pintará el ROI hasta que el punto inicial sea distinto de (-10, 10). Mira mousePressEvent!
    		if self.startPoint.x() != -10 and self.startPoint.y() != -10:
    
    			# En el API de Qt verás que la función drawRect recibe el punto inicial y el tamaño del rectangulo, no el punto inicial
    			# y el punto final. Por lo que estas dos instrucciones calculan el tamaño del ROI cada vez que se pinta.
    			dx = self.endPoint.x() - self.startPoint.x()
    			dy = self.endPoint.y() - self.startPoint.y()
    
    			# Pintamos el ROI con punto inicial en startPoint y dimensiones dx, dy
    			painter.drawRect(self.startPoint.x(), self.startPoint.y(), dx, dy)
    
    	# Cada vez que se pulsa un boton del raton, se llama a esta funcion
    	def mousePressEvent(self, event):
    		if(event.buttons() == Qt.LeftButton): 	# Si se ha pulsado el boton izquierdo
    			print("Left pressed")
    			# Nuestro punto de inicio del ROI será el punto donde esté el ratón justo cuando se pulsó el botón izquierdo
    			self.startPoint.setX(event.x())
    			self.startPoint.setY(event.y())
    		if(event.buttons() == Qt.RightButton):	# Si se ha pulsado el boton derecho
    			# Borramos el ROI haciendo sus coordenadas (-10, -10). PainEvent no dibuja rectangulo si el punto inicial es (-10, -10), recuerdas?
    			self.startPoint = QPoint(-10,-10)
    			self.endPoint = QPoint(-10,-10)
    			self.update()	# se llama a PaintEvent para que se borre el ROI que hubiera
    
    	# Cada vez que se libera un botón del ratón, se llama a esta función
    	def mouseReleaseEvent(self, event):
    		print("released")
    		# este será el punto final de nuestro ROI
    		self.endPoint.setX(event.x())
    		self.endPoint.setY(event.y())
    		print(self.startPoint, self.endPoint)
    
    	# Cada vez que se mueva el ratón se llamará a esta función. OJO! Si tienes el mouseTracking a True, el seguimiento se hará siempre que muevas el
    	# puntero por la ventana. Si pones mouseTracking a False (como en nuestro caso), sólo se llamará a esta función cuando ocurra otro evento de ratón
    	# como por ejemplo: mantener pulsado el botón izquierdo
    	def mouseMoveEvent(self, event):
    		print("Mouse moved")
    		# El punto final de nuestro ROI cambiará hasta que soltemos el botón izquierdo del ratón. De esta forma podemos ver visualmente
    		# como varia el tamaño del ROI mientras arrastramos el ratón con el botón izquierdo pulsado.
    		self.endPoint.setX(event.x())
    		self.endPoint.setY(event.y())
    		self.update()	# Repintamos cada vez que el ratón se mueva.
    
    
    	def closeEvent(self, event):
    		event.accept()
    	
    if __name__ == '__main__':
      
    	import sys
     
    	app = QApplication(sys.argv)
    	window = Window()
    	window.show()
    	sys.exit(app.exec_())
      
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
