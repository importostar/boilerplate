---
title: registros
date: 2020-05-07
---
Example Python program registros.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import csv
* import os
* import sqlite3
* import tkinter
* import modelos
* from modelos import Cliente
* #from registro_config import config 

## Methods

* def init():
* def save():
* def load():
* def create_field(window, label):
* def next():
* def previous():
* def new():
* def add_button(frame, t, command, side="left"):
* def warn_user(message):
* def show():
* def update():
* def main():

## Code

Python tkinter example

    import csv
    import os
    import sqlite3
    import tkinter
    
    import modelos
    from modelos import Cliente
    
    FILENAME = "exemplo.db"
    
    #    global name, age, address, phone, email, index
    
    #from registro_config import config 
    
    variaveis = {}
    
    
    def init():
        global con
        con = sqlite3.connect(FILENAME)
        Cliente.cria_tabela(con)
    
    def save():
        update()
        cliente.save(con)
            
    def load():
        global cliente
        try:
            cliente = Cliente.load(index, con)
        except IndexError:
            cliente = Cliente()
        
            
    def create_field(window, label):
        f1 = tkinter.Frame(window)
        f1.pack()
        variable = tkinter.Variable(window)
        l1 = tkinter.Label(f1, text=label)
        e1 = tkinter.Entry(f1, textvariable=variable)
        l1.pack(side="left")
        e1.pack(side="left")
        return variable
    
    def next():
        global index
        index += 1
        if index >= Cliente.last_id(con):
            index = 1
        load()
        show()
        
    def previous():
        global index
        index -= 1
        if index < 1:
            index = Cliente.last_id(con)
        load()
        show()
    
    def new():
        global index, cliente
        index = Cliente.last_id(con) + 1
        cliente = Cliente()
        show()
    
    def add_button(frame, t, command, side="left"):
        button = tkinter.Button(frame, text=t, command=command)
        button.pack(side="left")
    
    def warn_user(message):
        status_line["text"] = message
        status_line["fg"] = "red"
    
    def show():
        global index, cliente
        print(cliente)
        for field in Cliente.campos():
            var = variaveis[field["name"]]
            name = field["name"]
            var.set(getattr(cliente, name))
            
        status_line["text"] = str(index)
        status_line["fg"] = "black"
    
    def update():
        for field in Cliente.campos():
            var = variaveis[field["name"]]
            name = field["name"]
            setattr(cliente, name, var.get())
    
    def main():
        global index, status_line
        window = tkinter.Tk()
        for field in Cliente.campos():
            variaveis[field['name']] = create_field(window, field['label'])
        
        f3 = tkinter.Frame(window)
        f3.pack()
        add_button(f3, "<<", previous)
        add_button(f3, "Salvar", save)
        add_button(f3, "Novo", new)
        add_button(f3, ">>", next, side="right")
        
        status_line = tkinter.Label(window)
        status_line.pack()
        
        index = 1
        load()
        show()
        
        tkinter.mainloop()
    
    if __name__ == "__main__":
        init()
        main()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
