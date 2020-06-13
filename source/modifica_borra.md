---
title: modifica_borra
date: 2020-05-07
---
Example Python program modifica_borra.py

## Modules

* from tkinter import *
* from tkinter import ttk
* from tkinter import messagebox
* import sqlite3

## Classes

* class edicion():

## Methods

* def __init__(self, ventana):
* def conexion(self, consulta, parametros=()):
* def ver_datos(self):
* def format_grilla(self):
* def show_productos(self):
* def borrar_producto(self):
* def wish_delete(self):
* def editar(self):
* def modifica2(self, nuevo_prod, nombre, nuevo_precio, precio_viejo):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    from tkinter import messagebox
    
    import sqlite3
    
    
    class edicion():
        ##CONEXION A BASE DE DATOS SQLITE3##
        db_name= 'database.db'
    
    
        def __init__(self, ventana):
            self.ventana = ventana
            self.ventana.title("Modifica y Borra")
    
            ##GRILLA##
            self.formulario = ttk.Treeview(self.ventana, height = 7, columns = 2)
            self.formulario.grid(row=0, column=0, columnspan=2)
    
            self.formulario.heading('#0', text = 'Producto', anchor = CENTER)
            self.formulario.heading('#1', text = 'Precio', anchor = CENTER)
    
            ## MENSAJE LABEL##
            self.mensaje = Label(self.ventana, text = "", fg = "red")
            self.mensaje.grid(row=2, column=0, columnspan=4)
    
            ##CONTENEDOR##
            self.container = LabelFrame(self.ventana)
            self.container.grid(row=3, column=0, columnspan=3)
            boton1 = ttk.Button(self.container, text='Ver Datos', command=self.show_productos)
            boton2 = ttk.Button(self.container, text='Modifica Datos', command=self.editar)
            boton3 = ttk.Button(self.container, text='Borra Datos', command=self.borrar_producto)
            boton1.pack(side=LEFT, expand=True, fill=BOTH)
            boton2.pack(side=LEFT, expand=True, fill=BOTH)
            boton3.pack(side=LEFT, expand=True, fill=BOTH)
    
            self.format_grilla()
    
    
        ################################LOGICA###############################################
        ################################LOGICA###############################################
    
        def conexion(self, consulta, parametros=()):
            with sqlite3.connect(self.db_name) as conn:
                cursor = conn.cursor()
                result = cursor.execute(consulta, parametros)
                conn.commit()
            return result
    
        def ver_datos(self):
            consulta = 'SELECT * FROM product ORDER BY ID ASC'
            db_rows = self.conexion(consulta)
            for row in db_rows:
                self.formulario.insert('', 0, text=row[1], values=row[2])
    
        def format_grilla(self):
            grilla = self.formulario.get_children()
            for elementos in grilla:
                self.formulario.delete(elementos)
    
        def show_productos(self):
            grilla = self.formulario.get_children()
            for elementos in grilla:
                self.formulario.delete(elementos)
            consulta = 'SELECT * FROM product ORDER BY ID ASC'
            db_rows = self.conexion(consulta)
            for row in db_rows:
                self.formulario.insert('', 0, text=row[1], values=row[2])
    
    
        def borrar_producto(self):
            self.mensaje['text'] = ''
            try:
                self.formulario.item(self.formulario.selection())['text'][0]
            except IndexError as Error:
                self.mensaje['text'] = 'Seleccione un producto'
                return
            self.wish_delete()
    
        def wish_delete(self):
            MsgBox = messagebox.askquestion('Borrar Producto', '¿Esta seguro que desea borrar el producto?',
                                               icon='warning')
            if MsgBox == 'yes':
                self.mensaje['text'] = ''
                producto = self.formulario.item(self.formulario.selection())['text']
                consulta = 'DELETE FROM product WHERE Nombre = ?'
                self.conexion(consulta, (producto,))
                self.mensaje['text'] = 'Producto {} borrado correctamente'.format(producto)
                self.format_grilla()
                self.show_productos()
    
        def editar(self):
            self.mensaje['text'] = ''
            try:
                self.formulario.item(self.formulario.selection())['values'][0]
            except IndexError as error:
                self.mensaje['text'] = 'Seleccione un producto'
                return
            nombre = self.formulario.item(self.formulario.selection())['text']
            precio_viejo = self.formulario.item(self.formulario.selection())['values'][0]
            self.edimodi = Toplevel()
            self.edimodi.title = 'Modificar'
            Label(self.edimodi, text='Nuevo nombre:').grid(row=1, column=1)
            nuevo_prod = Entry(self.edimodi)
            nuevo_prod.focus()
            nuevo_prod.grid(row=1, column=2)
            ## NUEVO PRECIO ##
            Label(self.edimodi, text='Nuevo precio:').grid(row=3, column=1)
            nuevo_precio = Entry(self.edimodi)
            nuevo_precio.grid(row=3, column=2)
            Button(self.edimodi, text='Modificar', command=lambda: self.modifica2(nuevo_prod.get(), nombre,
            nuevo_precio.get(), precio_viejo)).grid(row=4, column=2, sticky=W)
            self.edimodi.grab_set()
            self.edimodi.wait_window()
            self.edimodi.mainloop()
    
        def modifica2(self, nuevo_prod, nombre, nuevo_precio, precio_viejo):
            consulta = 'UPDATE product SET Nombre = ?, Precio = ? WHERE Nombre = ? AND Precio = ?'
            parametros = (nuevo_prod, nuevo_precio, nombre, precio_viejo)
            self.conexion(consulta, parametros)
            self.edimodi.destroy()
            self.mensaje['text'] = 'Parametos modificados exitosamente'.format(nombre)
            self.show_productos()
    
    
    if __name__ == '__main__':
        ventana= Tk()
        aplicacion = edicion(ventana)
        ventana.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
