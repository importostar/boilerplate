---
title: gui hash
date: 2020-05-07
---
Example Python program gui-hash.py

## Modules

* import hashlib
* from tkinter import *
* from tkinter.ttk import *
* from tkinter.filedialog import askopenfilename

## Classes

* class ReadOnlyText(Text):

## Methods

* def compute_hashes(file_path, *hashes):
* def __init__(self, *args, **kwargs):
* def insert(self, *args, **kwargs):
* def toggle_state(self):

## Code

Python tkinter example

    import hashlib
    from tkinter import *
    from tkinter.ttk import *
    from tkinter.filedialog import askopenfilename
     
    # how to use checkbutton: https://stackoverflow.com/questions/4236910/getting-tkinter-check-box-state
     
    FOUR_KIBIBYTES = 2**10*4
     
    def compute_hashes(file_path, *hashes):
        hashes = [hashlib.new(hash) for hash in hashes]
        with open(file_path, 'rb') as f:
            data = f.read(FOUR_KIBIBYTES)
            while data:
                for i in range(len(hashes)):
                    hashes[i].update(data)  # if only python was multi-threaded.
                data = f.read(FOUR_KIBIBYTES)
            return [h.name +' '+ h.hexdigest() for h in hashes]
               
    class ReadOnlyText(Text):
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            self.configure(state=DISABLED)
       
        def insert(self, *args, **kwargs):
            was_disabled = False
            if self['state'] == DISABLED:
                was_disabled = True
                self.toggle_state()
            self.delete(1.0, END)
            super().insert(*args, **kwargs)
            if was_disabled:
                self.toggle_state()
       
        def toggle_state(self):
            if self['state'] == DISABLED:
                self.configure(state=NORMAL)
            else:
                self.configure(state=DISABLED)
               
     
    root = Tk()
    check_box_frame = Frame(root)
    checkboxes = []
     
    # create checkboxes
    for hash in hashlib.__all__:
        if any(map(hash.startswith, ('new', 'algo', 'shake', 'pbkdf'))):
            continue
        else:
            c = Checkbutton(check_box_frame, text=hash)
            c.state(['!alternate'])
            if hash == 'md5' or hash == 'sha1':
                c.state(['selected'])
            checkboxes.append(c)
       
    # arrange checkbox grid
    checkboxes.sort(key=lambda x: x['text'])
    row,col = 0,0
    for c in checkboxes:
        if col == 4:
            col = 0
            row += 1
        c.grid(row=row, column=col, sticky=W)
        col += 1
     
    check_box_frame.pack()
    display = ReadOnlyText(root, height=5, width=10)
    display.pack(fill=BOTH, expand=True)
     
    # prepare yourself for the crazy lazy
    start_button = Button(root, text='Browse', command=lambda:
                          display.insert(1.0,
                            '\n'.join(compute_hashes(
                              askopenfilename(initialdir='.'),
                              *[c['text'] for c in checkboxes if c.state()]
                            ))
                          )
                   ).pack()
                   
    edit_mode = Checkbutton(root, text='edit mode', command=display.toggle_state)
    edit_mode.state(['!alternate'])
    edit_mode.pack(side=RIGHT)
                   
    root.title('fort sumter')
    root.geometry('400x200')
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
