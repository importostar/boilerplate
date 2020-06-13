---
title: progressbar_threading
date: 2020-05-07
---
Example Python program progressbar_threading.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter as tk
* import tkinter.ttk as ttk
* import tkinter.messagebox as mbox
* import time
* from threading import *

## Methods

* def proceso(msg, pgbar):
* def click(pgbar):

## Code

Python tkinter example

    import tkinter as tk
    import tkinter.ttk as ttk
    import tkinter.messagebox as mbox
    import time
    from threading import *
    
    proceso_thread = None
    cuenta = 0
    
    
    def proceso(msg, pgbar):
        global cuenta
        print(msg, cuenta)
        time.sleep(5)
        pgbar.stop()
        pgbar.grid_forget()
        print('Termino')
    
    
    def click(pgbar):
        global proceso_thread
        global cuenta
        if not proceso_thread or not proceso_thread.isAlive():
            pgbar.grid(row=1, column=0, sticky='we', pady=10)
            pgbar.start(15)
            proceso_thread = Thread(target=proceso, args=[
                                    'Iniciando proceso', pgbar])
            proceso_thread.setDaemon(True)
            cuenta += 1
            proceso_thread.start()
        else:
            mbox.showwarning('Error', 'El proceso se esta ejecutando aun')
    
    
    if __name__ == "__main__":
        app = tk.Tk()
        app.title('Test progress bar')
        frm_app = tk.Frame(app)
        frm_app.grid(padx=10, pady=10)
        app.grid_rowconfigure(0, weight=1)
        app.grid_columnconfigure(0, weight=1)
        s = ttk.Style()
        s.theme_use('default')
        s.configure('TProgressbar', background='green')
        lbl_msg = tk.Label(frm_app, text='Por favor, espere...')
        lbl_msg.grid(row=0, column=0, sticky='we')
        pb_wait = ttk.Progressbar(
            frm_app, orient=tk.HORIZONTAL, length=200, mode='indeterminate')
        btn_start = tk.Button(frm_app, text='Iniciar',
                              command=lambda: click(pb_wait))
        btn_start.grid(row=2, column=0, sticky='we')
        app.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
