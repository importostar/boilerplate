---
title: webserver
date: 2020-05-07
---
Example Python program webserver.py

## Modules

* import Tkinter as tk
* import tkinter as tk   
* import tkinter.scrolledtext as tkscrolledtext
* import ScrolledText as tkscrolledtext
* import tkinter.filedialog as tkfiledialog
* import tkFileDialog as tkfiledialog
* import http.server as httpserver
* import SimpleHTTPServer as httpserver
* import socketserver as socketserver
* import SocketServer as socketserver
* import _thread as thread
* import thread as thread
* import os

## Classes

* class Application(tk.Frame):

## Methods

* def st_server():
* def verz(self):
* def start_server(self):
* def createWidgets(self):
* def __init__(self, master=None):

## Code

Python tkinter example

    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    """
    Webserver für Python
    03.01.2014 MH Quelltext für Python 2.7 und 3.x
    30.05.2013 MH Quelltext nach PEP8 überprüft
    http://creativecommons.org/licenses/by-nc-sa/3.0/de/
    """
    try:
        import Tkinter as tk
    except ImportError:
        import tkinter as tk   
    try:
        import tkinter.scrolledtext as tkscrolledtext
    except ImportError:
        import ScrolledText as tkscrolledtext
    try:
        import tkinter.filedialog as tkfiledialog
    except ImportError:
        import tkFileDialog as tkfiledialog
    try:
        import http.server as httpserver
    except ImportError:
        import SimpleHTTPServer as httpserver
    try:
        import socketserver as socketserver
    except ImportError:
        import SocketServer as socketserver
    try:
        import _thread as thread
    except ImportError:
        import thread as thread
    
    import os
    
    
    def st_server():
        """Start server"""
        while True:
            httpd.handle_request()
    
    
    class Application(tk.Frame):
    
        def verz(self):
            #select and change directory
            verzeichnis = tkfiledialog.askdirectory(
             title='Auswahl des Web-Rootverzeichnis')
            self.text.insert('end', verzeichnis)
            self.text.insert('end', "\n")
            if verzeichnis != '':
                os.chdir(verzeichnis)
    
        def start_server(self):
            thread.start_new_thread(st_server, ())
            self.start.config(state='disabled')
            self.text.insert('end', "Server gestartet mit PORT: {}\n".format(PORT))
    
        def createWidgets(self):
            """create GUI Tkinter"""
            #select directory
            self.verzeich = tk.Button(self)
            self.verzeich["text"] = "Startverzeichnis"
            self.verzeich["command"] = self.verz
            self.verzeich.pack({"side": "top", "fill": "x"})
    
            #start server
            self.start = tk.Button(self)
            self.start["text"] = "Startserver"
            self.start["fg"] = "green"
            self.start["command"] = self.start_server
            self.start.pack({"side": "top", "fill": "x"})
    
            #exit
            self.QUIT = tk.Button(self)
            self.QUIT["text"] = "Ende"
            self.QUIT["fg"] = "red"
            self.QUIT["command"] = self.quit
            self.QUIT.pack({"side": "top", "fill": "x"})
    
            #Information
            self.lab = tk.Label(self, text="Informationen")
            self.lab.pack({"side": "top"})
    
            self.text = tkscrolledtext.ScrolledText(self)
            self.text["width"] = 40
            self.text["height"] = 5
            self.text.pack({"side": "left"})
    
        def __init__(self, master=None):
            tk.Frame.__init__(self, master)
            self.pack(expand='yes')
            self.createWidgets()
    
    PORT = 8080
    Handler = httpserver.SimpleHTTPRequestHandler
    httpd = socketserver.TCPServer(("", PORT), Handler)
    root = tk.Tk()
    root.title("Webserver mit Python")
    app = Application(master=root)
    app.mainloop(){/code}

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
