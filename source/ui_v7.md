---
title: ui_v7
date: 2020-05-07
---
Example Python program ui_v7.py

## Modules

* import datetime
* import queue
* import logging
* import signal
* from tkinter import *
* from PIL import ImageTk
* from multiprocessing import Manager, Queue,Pool
* import PIL.Image
* from tkinter import filedialog
* import bussiness
* import multiprocessing
* import AutocompleteCombox
* import general
* import time
* from ListView2 import *
* from logger import *
* import alldevices
* from clientcomm_v1 import *
* import threading
* from tkinter.scrolledtext import ScrolledText
* from tkinter import ttk, VERTICAL, HORIZONTAL, N, S, E, W

## Classes

* class Clock(threading.Thread):
* class thread_with_trace(threading.Thread):
* class process_with_trace(multiprocessing.Process):
* class QueueHandler(logging.Handler):
* class ConsoleUi:
* class FormUi:
* class ThirdUi:
* class App:

## Methods

* def __init__(self):
* def run(self):
* def stop(self):
* def __init__(self, *args, **keywords):
* def start(self):
* def __run(self):
* def globaltrace(self, frame, event, arg):
* def localtrace(self, frame, event, arg):
* def kill(self):
* def __init__(self, *args, **keywords):
* def run(self):
* def kill(self):
* def __init__(self, log_queue):
* def emit(self, record):
* def __init__(self, frame):
* def display(self, record):
* def poll_log_queue(self):
* def __init__(self, frame):
* def connectwithplc(self):
* def initilization(self):
* def startprocess(self):
* def stopprocess(self):
* def force(self):
* def collectwritetaglist(self):
* def writetag(self,tagname_entered,tagvalue):
* def __init__(self,frame):
* def __init__(self, root):
* def quit(self, *args):
* def callallmotor1d(conn):
* def callallsov1s(conn):
* def main():

## Code

Python tkinter example

    import datetime
    import queue
    import logging
    import signal
    from tkinter import *
    from PIL import ImageTk
    from multiprocessing import Manager, Queue,Pool
    import PIL.Image
    from tkinter import filedialog
    import bussiness
    import multiprocessing
    import AutocompleteCombox
    import general
    import time
    from ListView2 import *
    from logger import *
    import alldevices
    from clientcomm_v1 import *
    import threading
    
    from tkinter.scrolledtext import ScrolledText
    from tkinter import ttk, VERTICAL, HORIZONTAL, N, S, E, W
    
    
    logger = logging.getLogger(__name__)
    
    
    
    
    
    class Clock(threading.Thread):
        """Class to display the time every seconds
        Every 5 seconds, the time is displayed using the logging.ERROR level
        to show that different colors are associated to the log levels
        """
    
        def __init__(self):
            super().__init__()
            self._stop_event = threading.Event()
    
        def run(self):
            logger.debug('Simulation started')
            while not self._stop_event.is_set():
                now = datetime.datetime.now()
                # level = logging.INFO
                # logger.log(level, now)
                time.sleep(1)
    
        def stop(self):
            self._stop_event.set()
    
    
    class thread_with_trace(threading.Thread):
        def __init__(self, *args, **keywords):
            threading.Thread.__init__(self, *args, **keywords)
            self.killed = False
    
        def start(self):
            self.__run_backup = self.run
            self.run = self.__run
            threading.Thread.start(self)
    
        def __run(self):
            sys.settrace(self.globaltrace)
            self.__run_backup()
            self.run = self.__run_backup
    
        def globaltrace(self, frame, event, arg):
            if event == 'call':
                return self.localtrace
            else:
                return None
    
        def localtrace(self, frame, event, arg):
            if self.killed:
                if event == 'line':
                    raise SystemExit()
            return self.localtrace
    
        def kill(self):
            self.killed = True
    
    class process_with_trace(multiprocessing.Process):
        def __init__(self, *args, **keywords):
            multiprocessing.Process.__init__(self, *args, **keywords)
            self.killed = False
    
            self.queue = multiprocessing.Queue()
    
    
        def run(self):
            self.process = multiprocessing.Process.start(self)
    
        def kill(self):
            self.process.terminate()
    
    
    class QueueHandler(logging.Handler):
        """Class to send logging records to a queue
        It can be used from different threads
        The ConsoleUi class polls this queue to display records in a ScrolledText widget
        """
        # Example from Moshe Kaplan: https://gist.github.com/moshekaplan/c425f861de7bbf28ef06
        # (https://stackoverflow.com/questions/13318742/python-logging-to-tkinter-text-widget) is not thread safe!
        # See https://stackoverflow.com/questions/43909849/tkinter-python-crashes-on-new-thread-trying-to-log-on-main-thread
    
        def __init__(self, log_queue):
            super().__init__()
            self.log_queue = log_queue
    
        def emit(self, record):
            self.log_queue.put(record)
    
    
    class ConsoleUi:
        """Poll messages from a logging queue and display them in a scrolled text widget"""
    
        def __init__(self, frame):
            self.frame = frame
            # Create a ScrolledText wdiget
            self.scrolled_text = ScrolledText(frame, state='disabled', height=12)
            self.scrolled_text.grid(row=0, column=0, sticky=(N, S, W, E))
            self.scrolled_text.configure(font='TkFixedFont')
            self.scrolled_text.tag_config('INFO', foreground='black')
            self.scrolled_text.tag_config('DEBUG', foreground='gray')
            self.scrolled_text.tag_config('WARNING', foreground='orange')
            self.scrolled_text.tag_config('ERROR', foreground='red')
            self.scrolled_text.tag_config('CRITICAL', foreground='red', underline=1)
            # Create a logging handler using a queue
            self.log_queue = queue.Queue()
            self.queue_handler = QueueHandler(self.log_queue)
            formatter = logging.Formatter('%(asctime)s: %(message)s')
            self.queue_handler.setFormatter(formatter)
            logger.addHandler(self.queue_handler)
            # Start polling messages from the queue
            self.frame.after(100, self.poll_log_queue)
    
        def display(self, record):
            msg = self.queue_handler.format(record)
            self.scrolled_text.configure(state='normal')
            self.scrolled_text.insert(tk.END, msg + '\n', record.levelname)
            self.scrolled_text.configure(state='disabled')
            # Autoscroll to the bottom
            self.scrolled_text.yview(tk.END)
    
        def poll_log_queue(self):
            # Check every 100ms if there is a new message in the queue to display
            while True:
                try:
                    record = self.log_queue.get(block=False)
                except queue.Empty:
                    break
                else:
                    self.display(record)
            self.frame.after(100, self.poll_log_queue)
    
    
    class FormUi:
    
        def __init__(self, frame):
            self.frame = frame
            self.listofwritetags = []
    
            self.button1 = ttk.Button(self.frame, text='Connect', command=self.connectwithplc)
            self.button1.grid(column=1, row=2, sticky=W,padx=5, pady=5)
            self.button2 = ttk.Button(self.frame, text='Initialization', command=self.initilization,state=DISABLED)
            self.button2.grid(column=1, row=3, sticky=W,padx=5, pady=5)
    
            self.button3 = ttk.Button(self.frame, text='Start', command=self.startprocess,state =DISABLED)
            self.button3.grid(column=1, row=4, sticky=W,padx=5, pady=5)
    
            self.button4 = ttk.Button(self.frame, text='Stop', command=self.stopprocess, state=NORMAL)
            self.button4.grid(column=1, row=5, sticky=W, padx=5, pady=5)
    
            self.button5 = ttk.Button(self.frame, text='Force', command=self.force, state=DISABLED)
            self.button5.grid(column=1, row=6, sticky=W, padx=5, pady=5)
    
    
    
        def connectwithplc(self):
    
            try:
                self.comm_object = general.General()
                self._elementlist = []
                self.tagvalueitemlist = []
                self.plc_cmd_list = []
                self.readsuccess = False
                self.eventtag = 'C1_LANCE2_LIFE'
    
            except Exception as e:
                level = logging.ERROR
                now = datetime.datetime.now()
                messege = "Error is " +str(e) + "from communication function"
                logger.log(level,messege)
                log_exception(e)
    
            finally:
                self.comm_sts = self.comm_object.sta_con_plc
                if self.comm_sts:
                    self.button1.config(text="Connected")
                    self.button2["state"] = NORMAL
                    level = logging.INFO
                    messege =  'Event:' + "PLC Simulation Successfully Connected"
                    logger.log(level, messege)
    
    
    
        def initilization(self):
            initial = "False"
    
            self.listofthread =[]
            self.listofprocess = []
    
            try:
                global devices
                self.listofwritetags = self.collectwritetaglist()
                conn1, conn2 = multiprocessing.Pipe()
                devices = bussiness.initilaztion(self.comm_object,logger)
                conn1.send(devices)
                self.callmotor1dprocess = multiprocessing.Process(target=callallmotor1d,args=[conn2])
                self.listofthread.append(self.callmotor1dprocess)
                self.callsov1sprocess =  multiprocessing.Process(target=callallsov1s,args=[conn2])
                self.listofthread.append(self.callsov1sprocess)
    
                self.button2.config(text="Initialized")
                initial = "True"
    
            except Exception as e:
                initial = "False"
                level = logging.INFO
                messege = 'Event:' + "Initialization Failed"
                logger.log(level, messege)
                logger.exception(e)
    
            finally:
                if initial:
                    self.button3["state"] = NORMAL
    
    
    
    
        def startprocess(self):
            for item in self.listofthread:
                item.start()
            self.button3.config(text="started")
    
    
    
        def stopprocess(self):
            for item in self.listofthread:
                item.kill()
    
        def force(self):
            win = tk.Toplevel(self.frame)
            win.geometry('300x100')
            ttk.Label(win,text = 'Choose Tag').grid(column=1,row = 0)
            tagname_entered = AutocompleteCombox.AutocompleteCombobox(win,width=20)
            tagname_entered.grid(column=1,row = 1)
            tagname_entered.set_completion_list(self.listofwritetags)
            tagname_entered.focus_set()
            ttk.Label(win, text='Enter Value').grid(column=2, row=0)
            value = IntVar()
            tagvalue =ttk.Entry(win,width=12,textvariable = value)
            tagvalue.grid(column=2, row=1)
            ttk.Label(win, text='Action').grid(column=2, row=3)
            action = ttk.Button(win,text = "Submit",command = self.writetag(tagname_entered,tagvalue))
            win.bind('<Control-Q>', lambda event=None: win.destroy())
            win.bind('<Control-q>', lambda event=None: win.destroy())
    
        def collectwritetaglist(self):
            list1 = []
            df = pd.read_excel(r'D:\OPCUA\Working_VF1.xls', sheet_name='WriteGeneral')
            n = 0
            while n < len(df.index):
                list1.append(n)
                n = n + 1
            return  list1
    
        def writetag(self,tagname_entered,tagvalue):
            tagname = str(tagname_entered.get())
            tagvalue = int(tagvalue.get())
            try:
                if len(tagname) > 3:
                    self.comm_object.writegeneral.writenodevalue(tagname, tagvalue)
                    level = logging.DEBUG
                    messege = tagname + " Force Value is " + str(tagvalue)
                    logger.log(level, messege)
    
            except Exception as e :
                log_exception(e)
                level = logging.ERROR
                messege = "Error is " +str(e) + "from Force function"
                logger.log(level, messege)
    
    
    class ThirdUi:
    
        def __init__(self,frame):
            self.frame = frame
            stim_filename = "smslogo.png"
            # create the PIL image object:
            PIL_image = PIL.Image.open(stim_filename)
            self.img = ImageTk.PhotoImage(file="smslogo.png")
            ttk.Label(self.frame, text='Progress Bar').pack(side=LEFT)
            self.progress = ttk.Progressbar(self.frame, orient=HORIZONTAL, length=500, mode='indeterminate')
            label=Label(self.frame, image =self.img)
            label.image = self.img
            Label.anchor=N
            self.progress.pack(side = LEFT)
            label.pack(side='right')
    
    
    
    
    
            # L = ttk.Label(self.frame, image=img)
    
    
    
    
    
    
    class App:
    
        def __init__(self, root):
            self.root = root
            root.title('SMS SIMULATION')
            root.columnconfigure(0, weight=1)
            root.rowconfigure(0, weight=1)
            # Create the panes and frames
            vertical_pane = ttk.PanedWindow(self.root, orient=VERTICAL)
            vertical_pane.grid(row=0, column=0, sticky="nsew")
            horizontal_pane = ttk.PanedWindow(vertical_pane, orient=HORIZONTAL)
            vertical_pane.add(horizontal_pane)
            form_frame = ttk.Labelframe(horizontal_pane, text="Control Panel")
            form_frame.columnconfigure(1, weight=1)
            horizontal_pane.add(form_frame, weight=1)
            console_frame = ttk.Labelframe(horizontal_pane, text="Console")
            console_frame.columnconfigure(0, weight=1)
            console_frame.rowconfigure(0, weight=1)
            horizontal_pane.add(console_frame, weight=1)
            third_frame = LabelFrame(vertical_pane, text="Third Panel")
            vertical_pane.add(third_frame, weight=1)
            # Initialize all frames
            self.form = FormUi(form_frame)
            self.console = ConsoleUi(console_frame)
            self.third = ThirdUi(third_frame)
            self.clock = Clock()
            self.clock.start()
            self.root.protocol('WM_DELETE_WINDOW', self.quit)
            self.root.bind('<Control-q>', self.quit)
            signal.signal(signal.SIGINT, self.quit)
    
        def quit(self, *args):
            self.clock.stop()
            self.root.destroy()
    
    
    def callallmotor1d(conn):
        devices = conn.recv()
        while True:
            bussiness.motorallprocessing(devices)
    
    
    
    
    def callallsov1s(conn):
        while True:
            devices = conn.recv()
            bussiness.allsov1processing(devices)
    
    
    
    
    
    def main():
        logging.basicConfig(level=logging.DEBUG)
        df = pd.read_excel(r'D:\OPCUA\Working_VF1.xls', sheet_name='Tag List')
        root = tk.Tk()
        app = App(root)
        app.root.mainloop()
    
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
