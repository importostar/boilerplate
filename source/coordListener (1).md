---
title: coordListener (1)
date: 2020-05-07
---
Example Python program coordListener (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import socket
* import json
* import Queue
* from thread import *
* from Tkinter import *
* from BaseHTTPServer import BaseHTTPRequestHandler
* from StringIO import StringIO

## Classes

* class HTTPRequest(BaseHTTPRequestHandler):
* class ResizingCanvas(Canvas):

## Methods

* def __init__(self, request_text):
* def send_error(self, code, message):
* def __init__(self,parent,**kwargs):
* def on_resize(self,event):
* def recievingThread(conn):
* def socketHandler():
* def convertPoint(point):
* def checkPointWindow(point):
* def checkQueue():

## Code

Python tkinter example

    # coding=utf-8
    import socket
    import json
    import Queue
    from thread import *
    from Tkinter import *
    
    '''
        HTTPRequest
        http://stackoverflow.com/questions/4685217/parse-raw-http-headers
        Använder pythons inbyggd httprequestbibliotek för att dela upp en sträng
        efter headers i http-format för enklare utbrytning av datat.
    '''
    from BaseHTTPServer import BaseHTTPRequestHandler
    from StringIO import StringIO
    
    class HTTPRequest(BaseHTTPRequestHandler):
        def __init__(self, request_text):
            self.rfile = StringIO(request_text)
            self.raw_requestline = self.rfile.readline()
            self.error_code = self.error_message = None
            self.parse_request()
    
        def send_error(self, code, message):
            self.error_code = code
            self.error_message = message
    
    # a subclass of Canvas for dealing with resizing of windows
    class ResizingCanvas(Canvas):
        def __init__(self,parent,**kwargs):
            Canvas.__init__(self,parent,**kwargs)
            print self.winfo_reqwidth(),self.winfo_reqheight()
            self.bind("<Configure>", self.on_resize)
    
        def on_resize(self,event):
            self.width = event.width
            self.height = event.height
            self.config(width=self.width, height=self.height)
    
    ## Variabler för anslutning
    ##TODO kanske låta användaren skriva in det här?
    host = ''
    while True:
        port = raw_input("Please enter a valid portnumber: ")
        try:
            port = int(port)
        except ValueError:
            print "Unvalid port please try again."
        else:
            print "Starting listening for input."
            break
    
    
    serversocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    ##  GUI
    guiUpdate = 500 ## Tid i millisekunder hur snabbt fönstret ska uppdatera sig för nya punkter
    windowSize = int(500),int(500)   ## Storlek på fönstret samt skalan på utskriften i form (x,y)
    windowMargin = int(10) ## Marginalen för sidorna i procent.
    top = Tk()          ## ansluter till tkinter objekt för utskrivning på en 2D-kanvas
    frame = Frame(top)
    frame.pack(fill=BOTH, expand=NO)
    window = ResizingCanvas(top, bg="green", width=windowSize[0], height=windowSize[1], highlightthickness=0);    ## Storleken på fönstret är 100x100 då
    top.wm_title("LineDrawer")
    top.configure(background='white')
    window.pack(fill=BOTH, expand=YES)
    ## koordinaterna högst kan vara 99 var
    coordQueue = Queue.Queue()  ## Kön för koordinaterna som utskrivningstråden letar i
    '''
        recievingThread tar emot data från sen socket och läser igenom detta som en HTTP-request
        den delar in requesten i headers och content och läser sedan av om content innehåller
        JSON-data, isåfall extraheras detta till en kö.
    
    '''
    def recievingThread(conn):
        while True:
            data = conn.recv(1024)
            print "i whileloopen" + data
            reply = '204 No Content'    ## Datat att skicka tillbaks (som en ack)
            if data:
                try:
                    request = HTTPRequest(data)
                    if request.command != 'PUT':
                        exit_thread("") ##TODO skicka tillbaka felmeddelande?
                    try:
                        ## Bryter ut headers och data från httprequesten
                        request.data_string = request.rfile.read(int(request.headers['Content-Length']))
                        coord = json.loads(request.data_string) ## Sätter in den utbrytna datasträngen i ett jsonobjekt
                    except Exception, e:
                        print "HTTP request parsing error" + e.message
    
                    print "testar datat som skickats in" + str(coord['X']) + ", " + str(coord['Y'])
                    ## jsondatat ska enbart innehålla två heltal mellan 0-100
                    if len(coord) is 2:
                        print "It is correctemundo jah"
                        tempCoord = (int(coord['X'])),(int(coord['Y']))
                        coordQueue.put(tempCoord) ## Sätter in den givna koordinaten i utskrivningskön
    
                except ValueError as msg:
                    print 'Error parsing json-string in http-document' + msg.message
    
            conn.sendall(reply) ## Skickar tillbaka ett meddelande till klienten som skickat requesten
            break
        conn.close()
    
    '''
        Trådad Loop som hanterar sockets,
    '''
    def socketHandler():
        while True: ##TODO körs för evigt
            conn, addr = serversocket.accept()
            print 'Connected to address: ' + addr[0]
            start_new_thread(recievingThread, (conn,))
        serversocket.close()
    
    ## Enkel funktion för att konverta en punkt från kanvasens yta till vanliga koordinater
    def convertPoint(point):
        temp = windowSize[0]/2 + point[0], windowSize[1]/2 - point[1]
        return temp
    
    '''
        startar och hanterar uppritningen som kollar utskrivningsköns värden
        varje sekund och går igenom den om det finns värden i den och skriver ut
        dessa på TKinter-kanvasen.
    '''
    prevpoint = None  ## Initierar variabel för föregående punkten
    first = True
    xMin, xMax, yMin, yMax = 0,0,0,0
    
    def checkPointWindow(point):
        global xMin, xMax, yMin, yMax
        if point[0] < xMin:
            xMin = point[0]
        elif point[0] > xMax:
            xMax = point[0]
    
        if point[1] < yMin:
            yMin = point[1]
        elif point[1] > yMax:
            yMax = point[1]
    
    def checkQueue():
        global first, prevpoint
        print "checking queue: " + str(coordQueue.qsize())
        if coordQueue.qsize() > 0:    ## Kom ihåg, under körning av många trådar kan qsize ge ett missvisande antal för längden på kön
            for i in range(0, coordQueue.qsize()):
                point = convertPoint(coordQueue.get(i))
                ## Finns det en tidigare uppsatt punkt på kanvasen så rita en linje mellan dessa
                if not first:
                    window.create_line(prevpoint,point);
                else:
                    first = False
                ## Rita upp en punkt i form av en oval på punkten
                window.create_oval(point[0]-2,point[1]-2,point[0]+2,point[1]+2, fill="red");
                prevpoint = point
        top.after(guiUpdate, checkQueue)  ## Kallar sig själv efter x millisekunder när den kört igenom sin grej
    try:
        serversocket.bind((host, port))
    except socket.error as msg:
        print 'Socket binding error.' + msg.message
        sys.exit()
    
    ## Initiera socket samt utskrivningsmetod
    serversocket.listen(5)
    top.after(guiUpdate, checkQueue); ## Hanterar körningen av köfunktionen då det är lite urballat att köra tkinter med trådar
                                ## och GUI
    ## Startar socketlyssningstråden
    start_new_thread(socketHandler, ())
    ## Initierar guiloopen när alla andra loopar och trådar initierats.
    top.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
