---
title: parcial3
date: 2020-05-07
---
Example Python program parcial3.py

## Modules

* import sympy
* import tkinter

## Classes

* class App(tkinter.Frame):

## Methods

* def __init__(self, master):
* def run(self):

## Code

Python tkinter example

    import sympy
    import tkinter
    
    
    class App(tkinter.Frame):
        def __init__(self, master):
            super().__init__(master)
            self.grid()
            self.vrs = sympy.symbols(
                'lambda,mu,rho,rho_0,Nbar,sigma^2,Qbar,Wbar,Tbar')
            self.rels = [
                sympy.Eq(self.vrs[2], self.vrs[0] / self.vrs[1]),
                sympy.Eq(self.vrs[3], 1 - self.vrs[2]),
                sympy.Eq(self.vrs[4], self.vrs[2] / self.vrs[3]),
                sympy.Eq(self.vrs[5], self.vrs[2] / (self.vrs[3]**2)),
                sympy.Eq(self.vrs[6], self.vrs[4] - self.vrs[2]),
                sympy.Eq(self.vrs[7], self.vrs[6] / self.vrs[0]),
                sympy.Eq(self.vrs[8], self.vrs[4] / self.vrs[0])
            ]
            tkinter.Label(self, text="M/M/1").grid(pady=10)
            self.vars = []
            for var in self.vrs:
                frame = tkinter.Frame(self)
                tkinter.Label(frame, text=sympy.pretty(var) + ':').grid()
                self.vars.append(tkinter.StringVar())
                tkinter.Entry(
                    frame, textvariable=self.vars[-1], width=20).grid(
                        column=1, row=0)
                frame.grid()
            tkinter.Button(self, text="Run", command=self.run).grid()
    
        def run(self):
            tmp = [(a, b) for a, b in zip(
                self.vrs, [float('0' + v.get()) for v in self.vars]) if b != 0]
            res = sympy.nonlinsolve([x.subs(tmp) for x in self.rels], self.vrs)
            for var, s in zip(self.vars, res.args[0].args):
                if s.is_Number:
                    var.set(s)
    
    
    root = tkinter.Tk()
    app = App(root)
    root.title("M/M/1")
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
