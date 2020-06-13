---
title: scrolled_canvas
date: 2020-05-07
---
Example Python program scrolled_canvas.py

## Modules

* from Tkinter import Canvas, GROOVE, BOTH, X, Y, YES, RIGHT, LEFT, W
* from ttk import Frame, Scrollbar, Checkbutton
* import logging
* import tkMessageBox
* import tkFont
* from Tkinter import Tk

## Classes

* class ScrolledCanvas(Frame):

## Methods

* def __init__(self, master, name=None, scrollregion=(0, 0, '5i', '5i'),
* def onLeftClick(item, event):

## Code

Python tkinter example

    from Tkinter import Canvas, GROOVE, BOTH, X, Y, YES, RIGHT, LEFT, W
    from ttk import Frame, Scrollbar, Checkbutton
    import logging
    import tkMessageBox
    
    
    class ScrolledCanvas(Frame):
        """
        A scrolling canvas of frames with checkboxes.
        """
        def __init__(self, master, name=None, scrollregion=(0, 0, '5i', '5i'),
                     items=[], window_size=[160, 30], **canvaskw):
            Frame.__init__(self, master, name=name)
    
            self.scrollcanvas = Canvas(self, name='scrollcanvas',
                                       scrollregion=scrollregion, **canvaskw)
            self.yscroll = Scrollbar(self, name='yscroll',
                                     command=self.scrollcanvas.yview)
            self.scrollcanvas['yscrollcommand'] = self.yscroll.set
            self.yscroll.pack(side=RIGHT, fill=Y)
            self.scrollcanvas.pack(side=LEFT, fill=BOTH, expand=YES)
            self.items = dict.fromkeys(items)
            for n, i in enumerate(items):
                self.items[i] = {'frame': Frame(self, name=(i.lower() + '_frame'))}
                self.items[i]['frame'].config(relief=GROOVE, padding=5)
                self.items[i]['chbx'] = Checkbutton(self.items[i]['frame'],
                                                        name=(i.lower() + '_chbx'))
                self.items[i]['chbx']['text'] = i
                self.items[i]['chbx'].pack(side=LEFT, fill=X)
                y = window_size[1] / 2 + window_size[1] * n
                self.items[i]['window'] = self.scrollcanvas.create_window(0, y)
                self.scrollcanvas.itemconfigure(self.items[i]['window'],
                                                window=self.items[i]['frame'],
                                                anchor=W, width=window_size[0],
                                                height=window_size[1])
    
    
    def onLeftClick(item, event):
            logging.debug(event.__dict__)
            if tkMessageBox.askokcancel('scrolled canvas', item):
                return
    
    
    if __name__ == "__main__":
        import tkFont
        from Tkinter import Tk
        dummy_items = ['holy grail', 'meaning of life', 'life of brian',
                       'jabberwocky', "monte python's flying circus",
                       'time bandits', 'brazil', '12 monkeys',
                       'adventures of baron von munchausen']
        root = Tk()
        maxstr = max(dummy_items, key=lambda x: len(x))
        pixsz = tkFont.Font().measure(maxstr)+25
        chrsz = len(maxstr)+5
        scrollcanvas = ScrolledCanvas(root, scrollregion=[0, 0, '5i', '3i'],
                                      items=dummy_items, height='2i',
                                      window_size=[pixsz, 30], width=pixsz)
        # add bindings?
        for item, val  in scrollcanvas.items.iteritems():
            logging.debug('binding frame %s', val['frame'])
            callback = lambda e, i=item: onLeftClick(i, e)
            val['frame'].bind('<Button-1>', callback)
        scrollcanvas.pack(expand=YES, fill=BOTH)
        scrollcanvas.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
