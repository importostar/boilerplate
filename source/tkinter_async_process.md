---
title: tkinter_async_process
date: 2020-05-07
---
Example Python program tkinter_async_process.py

## Modules

* import Tkinter
* import time
* import random
* import threading
* import Queue
* import sys
* One important thing to remember is that the thread has to yield

## Classes

* class GuiPart:
* class ThreadedClient:

## Methods

* def __init__(self, TkRoot, queue, endCommand):
* def processIncoming(self):
* def addStockToTrack(self):
* def get_quote(*args, **kwargs):
* def __init__(self, TkRoot):
* def periodicCall(self):
* def workerThread1(self):
* def endApplication(self):

## Code

Python tkinter example

    """
    This recipe describes how to handle asynchronous I/O in an environment where
    you are running Tkinter as the graphical user interface. Tkinter is safe
    to use as long as all the graphics commands are handled in a single thread.
    Since it is more efficient to make I/O channels to block and wait for something
    to happen rather than poll at regular intervals, we want I/O to be handled
    in separate threads. These can communicate in a threasafe way with the main,
    GUI-oriented process through one or several queues. In this solution the GUI
    still has to make a poll at a reasonable interval, to check if there is
    something in the queue that needs processing. Other solutions are possible,
    but they add a lot of complexity to the application.
    """
    import Tkinter
    import time
    import random
    import threading
    import Queue
    
    class GuiPart:
        def __init__(self, TkRoot, queue, endCommand):
            self.queue = queue
            self.QouteStr_var = Tkinter.StringVar()
    
            # Set up the GUI
            self.TkRoot = TkRoot
            self.myContainer1 = Tkinter.Frame(TkRoot)
            self.myContainer1.pack()
    
            # title name
            TkRoot.title("Stock App")
    
            console = Tkinter.Button(TkRoot, text='Done', command=endCommand)
            console.pack()
    
            # creates a frame inside myContainer1
            self.widgetFrame = Tkinter.Frame(self.myContainer1)
            self.widgetFrame.pack()
    
            # User enters stock symbol here:
            self.symbol = Tkinter.Entry(self.widgetFrame) 
            self.symbol.pack()
            self.symbol.focus_set()
    
            button1 = Tkinter.Button(self.myContainer1, command = self.addStockToTrack)
            self.myContainer1.bind("<Return>", self.addStockToTrack)
            button1.configure(text = "Add Symbol")
            button1.pack()  
    
    
        def processIncoming(self):
            """
            Handle all the messages currently in the queue (if any).
            """
            while self.queue.qsize():
                try:
                    msg = self.queue.get(0)
                    # Check contents of message and do what it says
                    # As a test, we simply print it
                    print msg
                    self.QouteStr_var.set( msg )
                    self.TkRoot.update_idletasks()  # KEYTAKEAWAY -- need to update the var value
                except Queue.Empty:
                    pass
    
        def addStockToTrack(self):
            s = self.symbol.get()
            self.symbol.delete(0, Tkinter.END)
            stockPrice = get_quote(s)
            self.QouteStr_var.set( s.upper() + ": " + str(stockPrice) )
            self.labelName = Tkinter.Label(self.myContainer1, textvariable = self.QouteStr_var )  # KEYTAKEAWAY -- Use special Tk StringVar to allow updates
            self.labelName.pack()
            #self.myContainer1.after(1000, get_quote)
    
    def get_quote(*args, **kwargs):
        time.sleep(rand.random() * 0.6)
        quote = rand.random()
        return quote
    
    
    class ThreadedClient:
        """
        Launch the main part of the GUI and the worker thread. periodicCall and
        endApplication could reside in the GUI part, but putting them here
        means that you have all the thread controls in a single place.
        """
        def __init__(self, TkRoot):
            """
            Start the GUI and the asynchronous threads. We are in the main
            (original) thread of the application, which will later be used by
            the GUI. We spawn a new thread for the worker.
            """
            self.TkRoot = TkRoot
    
            # Create the queue
            self.queue = Queue.Queue()
    
            # Set up the GUI part
            self.gui = GuiPart(TkRoot, self.queue, self.endApplication)
    
            # Set up the thread to do asynchronous I/O
            # More can be made if necessary
            self.running = 1
            self.thread1 = threading.Thread(target=self.workerThread1)
            self.thread1.start()
    
            # Start the periodic call in the GUI to check if the queue contains
            # anything
            self.periodicCall()
    
        def periodicCall(self):
            """
            Check every 100 ms if there is something new in the queue.
            """
            self.gui.processIncoming()
            if not self.running:
                # This is the brutal stop of the system. You may want to do
                # some cleanup before actually shutting it down.
                import sys
                sys.exit(1)
            #self.TkRoot.update_idletasks()
            self.TkRoot.after(100, self.periodicCall)
    
        def workerThread1(self):
            """
            This is where we handle the asynchronous I/O. For example, it may be
            a 'select()'.
            One important thing to remember is that the thread has to yield
            control.
            """
            while self.running:
                # To simulate asynchronous I/O, we create a random number at
                # random intervals. Replace the following 2 lines with the real
                # thing.
                time.sleep(rand.random() * 0.3)
                msg = rand.random()
                self.queue.put(msg)
    
        def endApplication(self):
            self.running = 0
    
    rand = random.Random()
    
    tkroot = Tkinter.Tk()
    client = ThreadedClient(tkroot)
    tkroot.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
