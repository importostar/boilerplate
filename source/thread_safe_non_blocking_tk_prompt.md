---
title: thread_safe_non_blocking_tk_prompt
date: 2020-05-07
---
Example Python program thread_safe_non_blocking_tk_prompt.py

## Modules

* import tkinter as tk
* import tkinter.messagebox as tkMessageBox
* import threading
* from queue import Queue
* # from view import prompt_start_thread, prompt, view

## Methods

* def prompt(title='', message='', message_type='INFO'):
* def prompt_start_thread(func, args=(), kwargs={}):
* def prompt_thread_loop(master):

## Code

Python tkinter example

    import tkinter as tk
    import tkinter.messagebox as tkMessageBox
    import threading
    from queue import Queue
    
    # Thread-safe version.
    # Tkinter functions are put into queue and called by prompt_thread_loop
    # in the main thread.
    
    messagebox_queue = Queue()
    
    
    def prompt(title='', message='', message_type='INFO'):
        if message_type == 'INFO':
            messagebox_queue.put((tkMessageBox.showinfo, (title, message), {}))
        elif message_type == 'ERROR':
            messagebox_queue.put((tkMessageBox.showerror, (title, message), {}))
    
    
    def prompt_start_thread(func, args=(), kwargs={}):
        threading.Thread(target=func, args=args, kwargs=kwargs).start()
    
    
    def prompt_thread_loop(master):
        try:
            while True:
                func, args, kwargs = messagebox_queue.get_nowait()
                func(*args, **kwargs)
        except:
            pass
        master.after(100, lambda: prompt_thread_loop(master))
    
    if __name__ == '__main__':
        root = tk.Tk()
        tkMessageBox.showinfo(message='blocking prompt')
        prompt_thread_loop(root)  # prompt_thread_loop is launched here
        prompt_start_thread(lambda: prompt(message='non blocking prompt'))
        label = tk.Label(root, text='code after the second prompt.')
        label.pack()
        root.mainloop()
    
        # 循环查询有无弹窗：
        # prompt_thread_loop(root)
        # 用法：
        # from view import prompt_start_thread, prompt, view
        # prompt_start_thread(lambda: prompt(message='asdf', master=view))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
