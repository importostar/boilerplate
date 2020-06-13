---
title: triangulacion
date: 2020-05-07
---
Example Python program triangulacion.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import Tkinter
* import ImageTk
* import numpy
* import math
* import time

## Classes

* class Transmisor:
* class Triangulation:

## Methods

*   def __init__(self, idnum, sstr = 100, scolor = "black"):
*   def draw(self, canvas, center):
*   def redraw(self, canvas, signal):
*   def __init__(self, canvas):
*   def run(self):
*   def trilateration(self, p):
*   def redraw(self, R1, R2, R3):
*   def distance(self, p1, p2):
* def onCanvasClick(event):

## Code

Python tkinter example

    #!/usr/bin/python
    
    import Tkinter
    import ImageTk
    import numpy
    import math
    import time
    
    w, h = 774, 548
    TRANS_IM = "transmisor.png"
    RECEP_IM = "receptor.png"
    
    ########################################################################
    #Clase usada para dibujar y manejar la posicion y otros atributos
    #usados en la simulacion de un transmisor.
    ########################################################################
    class Transmisor:
      
      ######################################################################
      #Inicializacion de variables.
      #*idnum Identificador numerico del transmisor
      #*sstr Signal Strength, fuerza de la senal hasta donde llega (en 
      # pixeles)
      #*scolor Color del circulo dibujado
      ######################################################################
      def __init__(self, idnum, sstr = 100, scolor = "black"):
        self.idnum = idnum
        self.sstr = sstr
        self.scolor = scolor
        self.widget = None
        self.label = None
        self.x, self.y = None, None
      
      ######################################################################
      #Metodo usado para dibujar inicialmente el circulo de la senal, su
      #etiqueta identificadora y la imagen del transmisor en un determinado
      #punto del canvas.
      #*canvas objeto canvas de Tkinter sobre el cual se dibujara
      #*center posicion en coordenadas de la pantalla (x, y) que sera
      # el centro del transmisor
      ######################################################################
      def draw(self, canvas, center):
        self.x, self.y = center
        self.widget = canvas.create_oval((self.x - self.sstr, self.y - self.sstr,
                                          self.x + self.sstr, self.y + self.sstr), 
                                          outline = self.scolor, width = 2.0)
        photo = ImageTk.PhotoImage(file = TRANS_IM)
        temp = Tkinter.Label(canvas, image = photo, anchor = "nw")
        temp.image = photo
        temp.place(x = self.x, y = self.y)
        self.label = Tkinter.Label(canvas, text = "%s"%self.idnum, background = self.scolor)
        self.label.place(x = self.x, y = self.y)
    
      ######################################################################
      #Redibujo del transmisor, en caso de haber un cambio en el receptor
      #y por ende su distancia hacia el transmisor.
      #*canvas objeto canvas de Tkinter sobre el cual se dibujaran los
      # cambios
      #*signal senal simulada calculada con la expansion del area del
      # transmisor.
      ######################################################################
      def redraw(self, canvas, signal):
        if self.widget is not None:
          if signal > self.sstr:
            signal = self.sstr
          canvas.coords(self.widget, (self.x-signal, self.y-signal, self.x+signal, self.y+signal))
          #canvas.update()
          return
        else:
          raise TypeError("La Transmisor es None. Primero se debe dibujar antes de ajustar.")
    
    ######################################################################
    #Clase usada para manejar los transmisores, y los calculos que
    #se hacen en base a estos para obtener la localizacion de un
    #receptor determinado.
    ######################################################################
    class Triangulation:
    
      ######################################################################
      #Inicializacion, se crean los tres transmisores con sus respectivos
      #ID's, fuerzas de senal y colores.
      #*canvas objeto canvas sobre el cual se dibujaran los transmisores
      ######################################################################
      def __init__(self, canvas):
        self.A1 = Transmisor(idnum = 1, sstr = 400, scolor = 'red')
        self.A2 = Transmisor(idnum = 2, sstr = 400, scolor = 'green2')
        self.A3 = Transmisor(idnum = 3, sstr = 400, scolor = 'blue')
        self.canvas = canvas
    
      ######################################################################
      #Metodo para iniciar la simulacion. Define 3 puntos sobre los cuales
      #se colocaran los transmisores, los dibuja sobre el canvas y 
      #calcula la localizacion de un punto predefindo.
      #Retorna:
      #*p Punto donde se encuentra el receptor.
      ######################################################################
      def run(self):
        c1 = 263, 485
        c2 = 708, 393
        c3 = 512, 81
        self.A1.draw(self.canvas, c1)
        self.A2.draw(self.canvas, c2)
        self.A3.draw(self.canvas, c3)
        p = w/2, h/3
        self.trilateration(p)
        return p
    
      ######################################################################
      #Calculo de la triangulacion usando el algoritmo de trilateracion.
      #Si el receptor esta al alcance de tres transmisores calcula su
      #posicion exacta, si solo esta al alcance de dos, calcula una posicion
      #con error ligero, y si solo esta al alcance de una, no puede
      #calcularlo
      #* p Punto al cual se calculara su posicion (solo usado para conocer
      # donde detener el desplazamiento de la senal con los transmisores)
      ######################################################################
      def trilateration(self, p):
        P1 = numpy.array([self.A1.x, self.A1.y])
        P2 = numpy.array([self.A2.x, self.A2.y])
        P3 = numpy.array([self.A3.x, self.A3.y])
        ex = (P2 - P1)/(numpy.linalg.norm(P2 - P1))
        i = numpy.dot(ex, P3 - P1)
        ey = (P3 - P1 - i*ex)/(numpy.linalg.norm(P3 - P1 - i*ex))
        ez = numpy.cross(ex,ey)
        d = numpy.linalg.norm(P2 - P1)
        j = numpy.dot(ey, P3 - P1)
        R1 = self.distance((self.A1.x, self.A1.y), p)
        R2 = self.distance((self.A2.x, self.A2.y), p)
        R3 = self.distance((self.A3.x, self.A3.y), p)
        x = (pow(R1,2) - pow(R2,2) + pow(d,2))/(2*d)
        y = ((pow(R1,2) - pow(R3,2) + pow(i,2) + pow(j,2))/(2*j)) - ((i/j)*x)
        z = None
        try:
          z = math.sqrt(pow(R1,2) - pow(x, 2) - pow(y, 2))
          tri = P1 + x*ex + y*ey + z*ez
          print "Punto localizado en:", tri
          if z > 0:
            print "Se encontro la solucion con dos antenas"
          elif z == 0:
            print "Se encontro la solucion con las tres antenas"
        except ValueError:
          print "No existe solucion a el punto "
        print
        self.redraw(R1, R2, R3)
        return
    
      ######################################################################
      #Redibujo de las senaales progresivamente
      #* R1 distancia total a ajustar senal del primer transmisor
      #* R2 distancia total a ajustar senal del segundo transmisor
      #* R3 distancia total a ajustar senal del tercer transmisor
      ######################################################################
      def redraw(self, R1, R2, R3):
        for i in range(1, int(max(R1, R2, R3)), 3):
          if i <= R1:
            self.A1.redraw(self.canvas, i)
          if i <= R2:
            self.A2.redraw(self.canvas, i)
          if i <= R3:
            self.A3.redraw(self.canvas, i)  
          self.canvas.update()
          time.sleep(0.01)
        
      ######################################################################
      #Calculo de la senal, simulado midiendo un desplazamiento del area
      #de los circulos de los transmisores hasta el receptor.
      #* p1 posicion del receptor (para simular donde se detiene la senal
      #porque encontro un receptor).
      #* p2 posicion del transmisor
      ######################################################################
      def distance(self, p1, p2):
        x1, y1 = p1
        x2, y2 = p2
        return math.sqrt( (y2 - y1)**2 + (x2 - x1)**2)
    
    def onCanvasClick(event):
      global receptor, canvas
      receptor.destroy()
      photo2 = ImageTk.PhotoImage(file = RECEP_IM)
      receptor = Tkinter.Label(canvas, image = photo2)
      receptor.image = photo2
      receptor.place(x = event.x, y = event.y)
      print 'Punto del receptor:', event.x, event.y
      tri.trilateration((event.x, event.y))
    
    if __name__ == "__main__":
      root = Tkinter.Tk()
      root.title('Triangulacion')
      canvas = Tkinter.Canvas(root, width = w, height = h, background = None)
      photo = ImageTk.PhotoImage(file = "MAP.png")
      bg = canvas.create_image(0, 0, image = photo, anchor = "nw")
    
      tri = Triangulation(canvas)
      x, y = tri.run()
    
      photo2 = ImageTk.PhotoImage(file = RECEP_IM)
      receptor = Tkinter.Label(canvas, image = photo2)
      receptor.image = photo2
      receptor.place(x = x, y = y)
    
      canvas.tag_bind(bg, '<Button-1>', onCanvasClick)
      canvas.pack()
      root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
