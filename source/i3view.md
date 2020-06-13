---
title: i3view
date: 2020-05-07
---
Example Python program i3view.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* import os
* import re
* ''' parse important lines from i3 config '''

## Classes

* class sequence:
* class Tabuler:

## Methods

* def always(v):
* def astuple(o:sequence) -> tuple:
* def zipo(l,v=always(None)):
* def zipdef(a,b,z=lambda: None):
* def __init__(self, sep="|", pad=2):
* def insert(self, row):
* def insertmany(self, rows):
* def rewidth(self, row):
* def format(self):
* def prn(self):
* def __repr__(self):
* def __str__(self):
* def deformat(string, values, zero=''):
* # def reform(l) -> str:
* def parse(config:[str]) -> list:
* def tabulize(rows) -> [str]:
* def viewer(bindings) -> tkinter.Tk:
* def main():
* def t0():

## Code

Python tkinter example

    #!/usr/bin/env python
    
    import tkinter
    import os
    import re
    
    #####################################################################  prelude
    
    def always(v):
        '''function always returning the same value (see clojure `constantly`)'''
        return lambda *a,**k: v
    
    class sequence:
        ''' dummy class to have type named sequence '''
        pass
    
    def astuple(o:sequence) -> tuple:
        '''turns a sequence into a tuple'''
        t = type(o)
        if t == list:
            return tuple(o)
        elif t == tuple:
            return o
        else:
            raise TypeError(f'{o} should be list or tuple')
    
    def zipo(l,v=always(None)):
        '''always . zip'''
        return zip(l, map(lambda e: v(), l))
    
    def zipdef(a,b,z=lambda: None):
        ''' zip that fills missing tail with a default value '''
        la = len(a)
        lb = len(b)
        lim = max(la,lb)
        beg = min(la,lb)
        yield from zip(a[:lim], b[:lim])
        yield from zipo(a[beg:], z) if la > lb else zipo(b[beg:], z)
    
    #####################################################################  classes
    
    class Tabuler:
        '''generate constant width table formatting'''
    
        def __init__(self, sep="|", pad=2):
            self.sep = sep
            self.pad = pad
            self.rows = []
            self.width = 0
            self.widths = []
    
        def insert(self, row):
            self.rows.append(row)
            self.rewidth(row)
    
        def insertmany(self, rows):
            for row in rows:
                self.insert(row)
    
        def rewidth(self, row):
            '''
            - invariant: width = max len(row)
            - invariant: widths = [max len(cell) ...]
            '''
            l = len(row)
            self.width = max(self.width, l)
            pairs_of_widths = zipdef(self.widths,[len(str(e)) for e in row], always(0))
            self.widths = [max(a,b) for a,b in pairs_of_widths]
    
        def format(self):
            ''' widths -> format string '''
            return self.sep.join(f'%0{w}s' for w in self.widths)
    
        def prn(self):
            return [deformat(self.format(), row) for row in self.rows]
    
        def __repr__(self):
            return str(self)
    
        def __str__(self):
            return f'<Table {len(self.rows)} {self.width} {self.widths}>'
    
    #####################################################################  functions
    
    def deformat(string, values, zero=''):
        '''helper to apply formating % on arg of variable length'''
        varcount = len(re.findall('%', string))
        valcount = len(values)
        values = astuple(values)
        if varcount == valcount:
            return string % values
        elif varcount < valcount:
            return string % values[:varcount]
        else:
            fillers = tuple(zero for _ in range(varcount-valcount))
            return string % (values + fillers)
    
    # def reform(l) -> str:
    #     '''helper to parse i3 config lines'''
    #     [_, binding, *cmd] = l.strip().split(' ')
    #     cmd = ' '.join(cmd)
    #     return f'{binding} :: {cmd}'
    
    def parse(config:[str]) -> list:
        ''' parse important lines from i3 config '''
        pattern = r'^bindsym.*exec.*'
        for line in config:
            if re.match(pattern, line):
                [_, b, *c] = line.strip().split(' ')
                yield b, *c
    
    def tabulize(rows) -> [str]:
        ''' uses tabuler to format rows '''
        t = Tabuler(sep=" | ")
        t.insertmany([b,*c] for [b,*c] in rows)
        return t.prn()
    
    def viewer(bindings) -> tkinter.Tk:
        v = tkinter.Tk()
        v.title('i3 config bindings')
        s = tkinter.Scrollbar(v)
        s.pack(side=tkinter.RIGHT,fill=tkinter.Y)
        l = tkinter.Listbox(v, yscrollcommand=s.set)
        for b in bindings:
            l.insert(tkinter.END, b)
        l.pack(side=tkinter.LEFT, fill=tkinter.BOTH, expand=tkinter.YES)
        s.config(command=l.yview)
        return v
    
    #####################################################################  main
    
    CONFIG='~/.config/i3/config'
    
    def main():
        CFG = os.path.expanduser(CONFIG)
        with open(CFG) as cfg:
            bs = parse(cfg)
            ls = tabulize(bs)
            v = viewer(ls)
            v.mainloop()
    
    if __name__ == '__main__':
        main()
    
    #####################################################################  tests
    
    def t0():
        inputs = [
            [1,0],
            [1,2,0],
            [1,1],
            [100,0]
        ]
        t = Tabuler(sep=" | ")
        for i in inputs:
            t.insert(i)
        print('\n'.join(t.prn()))
        return t
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
