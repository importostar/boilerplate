---
title: non_blocking_tkinter
date: 2020-05-07
---
Example Python program non_blocking_tkinter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import io, base64
* from PIL import Image, ImageTk
* import tkinter
* from datetime import datetime
* import time
* import io, base64
* from PIL import Image, ImageTk
* import tkinter as tk
* from datetime import datetime
* import time
* import threading
* import queue

## Classes

* class MyCustomWindow1(tkinter.Toplevel):
* class MyCustomWindow2(tkinter.Toplevel):
* class App(tkinter.Tk):
* class WinNotify():

## Methods

* def __init__(self, root):
* def __init__(self, root):
* def __init__(self):
* def x(self, cor):
* def y(self):
* def listen_for_result(self):
* def __init__(self):
* def thread_function(self):
* def mudarCor(self, cor):

## Code

Python tkinter example

    import io, base64
    from PIL import Image, ImageTk
    import tkinter
    from datetime import datetime
    import time
    
    
    import io, base64
    from PIL import Image, ImageTk
    import tkinter as tk
    from datetime import datetime
    import time
    import threading
    import queue
    
    
    """
    root = tkinter.Tk()
    root.withdraw()
    
    top = tkinter.Toplevel(root, bg='red')
    top2 = tkinter.Toplevel(root, bg='green')
    
    #to display root window again
    #root.iconify()
    #root.deiconify()
    root.mainloop()
    
    exit()
    """
    class MyCustomWindow1(tkinter.Toplevel):
        def __init__(self, root):
            tkinter.Toplevel.__init__(self)
            self['background'] = '#2b2b2b'
    
            print('janela')
    
    class MyCustomWindow2(tkinter.Toplevel):
        def __init__(self, root):
            tkinter.Toplevel.__init__(self)
            self['background'] = '#ff0000'
            print('janela')
            self.thread_queue = queue.Queue()
    
    
            logo_b64 = b'''
            iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAIA
            AAAlC+aJAAAA/0lEQVR4nO3Zyw7CMAxEUdP//+W2rCqBoJA2noclS1kn9yjLeex7xKY76+
            wNS+l6KSCjXgdIqhcB8uoVgNR6OiC7ngsA1BMBmHoWAFZPASDr8QBwPRiAr0cCKPUwAKse
            AyDWAwDc+mwAvT4VoKjPA4jqkwC6+gyAtD7WSYC6fu4HDOonAB71dwE29bcATvXXAWb1Fw
            F+9VcAlvXDANf6MYBx/QDAu/4fwL7+J6BC/TmgSP0JoE79N0Cp+g9Atfp3QMH6F0DN+gNQ
            tj62WErXB2PgQNZLAb3U6wC91OsAvdTrAL3U6wC91OsAvdTrAL3U6wC91OsAvdTrAL3Uz7
            z+BNmX4gqbppsaAAAAAElFTkSuQmCC
            '''
            # Decode the PNG data & "wrap" it into a file-like object
            fh = io.BytesIO(base64.b64decode(logo_b64))
    
            # Create a PIL image from the PNG data
            img = Image.open(fh, mode='r')
    
            photo = ImageTk.PhotoImage(image=img)
            self.img= tk.Label(root, image=photo)
    
            self.img.image = photo
            self.img.pack()
    
    class App(tkinter.Tk):
    
        def __init__(self):
            tkinter.Tk.__init__(self)
            self.win1 = MyCustomWindow1(self)
            self.win2 = MyCustomWindow2(self)
            print('a')
            #self.update_idletasks()
    
        def x(self, cor):
            self.win2['background'] = cor
            #self.win2['background'] = '#0000ff'
    
        def y(self):
            self.mainloop()
    
        def listen_for_result(self):
            """ Check if there is something in the queue. """
    
            try:
                self.res = self.thread_queue.get(0)
                self._print(self.res)
            except queue.Empty:
                self.after(100, self.listen_for_result)
    
    class WinNotify():
        def __init__(self):
            x = threading.Thread(target=self.thread_function)
            x.start()
    
        def thread_function(self):
            self.app = App()
            self.app.mainloop()
    
        def mudarCor(self, cor):
            self.app.x(cor)
    
    
    a = WinNotify()
    
    cnt = 0
    while True:
        time.sleep(3)
        print(cnt)
        if cnt == 0:
            a.mudarCor('#0000ff')
        elif cnt == 1:
            a.mudarCor('#00ff00')
        elif cnt == 2:
            a.mudarCor('#ff0000')
        elif cnt == 4:
            a.mudarCor('#ffaaaa')
        else:
            a.mudarCor('#aaaaaa')
    
        cnt += 1
        pass
    print('depois')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
