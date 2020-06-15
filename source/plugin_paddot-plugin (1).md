---
title: plugin_paddot plugin (1)
date: 2020-05-07
---
Example Python program plugin_paddot-plugin (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from Tkinter import *
* import os
* import glob
* import tkMessageBox
* import tkFileDialog
* import matplotlib as mpl
* from math import sqrt
* from pymol import cmd
* import platform
* import pwd
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
* from matplotlib.figure import Figure
* import matplotlib
* from . import matplotlib_fix_prefs
* from matplotlib.backends import backend_tkagg
* import pymol
* import Tkinter as Tk
* from matplotlib.figure import Figure
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, FigureManagerTkAgg

## Classes

* class Pdb():
* class Grap():
* class GUI():

## Methods

* def __init__(self):
* def __init__(self):
* def pross(self, key, save_dir, rmsd):
* def __init__(self, parent):
* def overload(self):
* def _new_figure_manager(num, *args, **kwargs):
* def preg(self, ventana, parent):
* def askcls():
* def plot(self, minn, maxx):
* def __init__(self, menu):
* def plot(self, minn, maxx):
* def loadtemplate(self, cnv, frme, arr, parent):
* def savedir(self):
* def checkbtn(self, ste, chkdlg):
* def ok(self, clustr, parent, rmsd):
* def visual(self, uno):
* def cerrar(parent):
* def selec(self):

## Code

Python tkinter example

    from Tkinter import *
    import os
    import glob
    import tkMessageBox
    import tkFileDialog
    import matplotlib as mpl
    from math import sqrt
    from pymol import cmd
    import platform
    import pwd
    
    mpl.use("TkAgg")
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
    from matplotlib.figure import Figure
    
    
    def __init__(self):
        # Funcion que agrega el nombre a la barra de pymol
        self.menuBar.addmenuitem('Plugin', 'command', 'PADDOT-plugin', label='PADDOT-plugin',
                                 command=lambda: GUI(self.menuBar))
    
    
    class Pdb():
        def __init__(self):
            self.fbe_list = []
            self.fbe_listL = []
            self.fbe_listA = []
            self.fbe_min = []
            self.fbe_max = []
    
        # self.pl_lst = []
    
        def pross(self, key, save_dir, rmsd):
            try:
                file = open(key, "r")
                wrt = file.name
                wrt = wrt.replace("dlg", "pdb")
            except:
                print "Error"
    
            try:
                doc = open(save_dir + "/" + wrt, "w")
    
            except:
                doc = open(wrt, "w")
                tkMessageBox.showinfo("Advertencia", "El trabajo se guardara en " + str(os.getcwd()))
    
            searchstrings = ("DOCKED: MODEL", "DOCKED: ATOM",
                             "DOCKED: USER    Estimated Free Energy of Binding", "DOCKED: TER")
            list_of_list = []
            temp_list = []
            for line in file.readlines():
                for word in searchstrings:
                    if word in line:
                        incoming_data = []
                        if word == "DOCKED: MODEL":
                            incoming_data.extend(line.split())
                            temp_list.append(incoming_data[2])
                            line2 = line.replace("DOCKED: ", "")
                            doc.writelines(line2)
                            del incoming_data[:]
                        elif word == "DOCKED: USER    Estimated Free Energy of Binding":
                            incoming_data.extend(line.split())
                            temp_list.append(incoming_data[-3])
                            self.fbe_list.append(float(incoming_data[-3]))
                            line2 = line.replace("DOCKED: ", "")
                            doc.writelines(line2)
                            del incoming_data[:]
                        elif word == "DOCKED: ATOM":
                            incoming_data.extend(line.split())
                            del incoming_data[:1]
                            temp_list.append(" ".join(incoming_data))
                            del incoming_data[:]
                            line2 = line.replace("DOCKED: ", "")
                            lne = line2.replace("A", "C")
                            lne = lne.replace("CTOM", "ATOM")
                            doc.writelines(lne)
                        elif word == "DOCKED: TER":
                            incoming_data.extend(line.split())
                            del incoming_data[0]
                            temp_list.append(incoming_data[0])
                            del incoming_data[:]
                            list_of_list.append(temp_list[:])
                            del temp_list[:]
                            line2 = line.replace("DOCKED: ", "")
                            doc.writelines(line2)
                            doc.writelines("ENDMDL\n")
            self.fbe_listL.extend(self.fbe_list)
            self.fbe_listA.append(self.fbe_list)
            doc.close()
            temp_elist = []
            scn_tmp_list = []
            scn_list_list = []
            list_elem = len(list_of_list)
            #print list_of_list
            for con in range(0, list_elem):
                for elem in list_of_list[con]:
                    thiss = elem.split()
                    if 1 < len(thiss) < 13:
                        temp_elist.extend(thiss[5:8])
                    elif len(thiss) == 13:
                        temp_elist.extend(thiss[6:9])
                temp_elist = [float(i) for i in temp_elist]
                scn_tmp_list.append(temp_elist[:])
                print 'elementos en el arreglo', len(scn_tmp_list)
                #print temp_elist[:]
                del temp_elist[:]
            #print "======================="
            print scn_tmp_list[:]
            contador = 0;
            #print "Comienzo", contador,  scn_tmp_list[:]
            contador += 1
            scn_list_list = scn_tmp_list[:]
            del scn_tmp_list[:]
            fbe_less = float(list_of_list[0][1])
            fbe_index = 0
            index_list = []
            index_list_list = []
    
            while len(scn_list_list) > 0:
                #print scn_list_list[0]
                lista_a = scn_list_list[0]
                #print scn_list_list[0]
                rng_lista = len(lista_a)
                index_list.append(list_of_list[0][0])
                cont = 0
                del scn_list_list[0]
                del list_of_list[0]
                while cont < len(scn_list_list):
                    lista_b = scn_list_list[cont]
                    sumatoria = 0.0
                    for el in range(0, rng_lista):
                        sumatoria += (float(lista_a[el]) - float(lista_b[el])) ** 2.0
                    rmsd = sqrt(sumatoria / rng_lista)
                    print rmsd,
                    # if rmsd <= float(rmsdtxt.get()): Linea original sin poder usar el textbox
                    if rmsd <= 2.0:
                        # linea con hardcode
                        index_list.append(list_of_list[cont][0])
                        del scn_list_list[cont]
                        del list_of_list[cont]
                    cont -= 1
                    cont += 1
                index_list_list.append(index_list[:])
                #print "lista", index_list_list[:]
                index_list = []
            self.fbe_min = min(self.fbe_listL)
            self.fbe_max = max(self.fbe_listL)
            return self.fbe_min, self.fbe_max
            # os.chdir(self.dirct)
    
    
    class Grap():
        '''Clase que se encarga de graficar todo lo visual usando matplotlib'''
    
        def __init__(self, parent):
            self.parent = parent
            self.parent.withdraw()
            self.nw_root = Tk()
        """
        '''
        PyMOL matplotlib integration
        matplotlib uses Tk, which conflicts with the PyMOL Tk mainloop. This module
        overloads the TkAgg backend to use PyMOLs Tk instance as master widget.
        This is likely to be fragile against matplotlib upgrades.
        (c) 2012 Thomas Holder, MPI for Developmental Biology
        License: BSD-2-Clause
        '''
        def overload(self):
            import matplotlib
            from . import matplotlib_fix_prefs
            if matplotlib_fix_prefs['verbose']:
                print ' matplotlib_fix: If you have issues with matplotlib and PyMOL, check'
                print ' matplotlib_fix: the values of psico.matplotlib_fix_prefs'
            if matplotlib_fix_prefs['force_tkagg']:
                matplotlib.use('TkAgg')
            if matplotlib.get_backend() != 'TkAgg':
                return
            if not matplotlib_fix_prefs['tkagg_overload']:
                return
            from matplotlib.backends import backend_tkagg
            def _new_figure_manager(num, *args, **kwargs):
                import pymol
                if pymol._ext_gui is None:
                    return new_figure_manager(num, *args, **kwargs)
                    backend_tkagg.show._needmain = False
                import Tkinter as Tk
                from matplotlib.figure import Figure
                from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, FigureManagerTkAgg
                FigureClass = kwargs.pop('FigureClass', Figure)
                figure = FigureClass(*args, **kwargs)
                window = Tk.Toplevel(master=pymol._ext_gui.root)
                canvas = FigureCanvasTkAgg(figure, master=window)
                figManager = FigureManagerTkAgg(canvas, num, window)
                if matplotlib.is_interactive():
                    figManager.show()
                return figManager
                new_figure_manager = backend_tkagg.new_figure_manager
                backend_tkagg.new_figure_manager = _new_figure_manager
        try:
            overload()
        except:
            print 'matplotlib_fix failed'
        # vi:expandtab:smarttab
        """
    
        def preg(self, ventana, parent):
            self.nw_root = ventana
            self.parent = parent
    
            def askcls():
                if tkMessageBox.askokcancel("Quit", "Quieres cerrar la ventana?"):
                    self.nw_root.destroy()
                    self.parent.deiconify()
    
            self.nw_root.protocol("WM_DELETE_WINDOW", askcls)
    
        def plot(self, minn, maxx):
            self.fig = Figure(figsize=(4, 4), dpi=100)
            self.grad = self.fig.add_axes([0.05, 0.80, 0.9, 0.05])
            self.colr = mpl.cm.cool
            self.norm = mpl.colors.normalize(vmin=minn, vmax=maxx)
            cb1 = mpl.colorbar.ColorbarBase(self.grad, cmap=self.colr, norm=self.norm, orientation=
            "horizontal")
            self.canvas = FigureCanvasTkAgg(self.fig, master=self.nw_root).show()
            self.canvas.get_tk_widget().pack(side=TOP, fill=BOTH, expand=1)
            return self.nw_root
    
    
    class GUI():
        def __init__(self, menu):
            # parent = app.root
            self.menuBar = menu
            self.sistm = platform.system()
            self.usr = pwd.getpwuid(os.geteuid()).pw_name
            if self.sistm == 'Linux' or self.sistm == 'Linux2':
    
                self.dir = "/home/" + self.usr + "/.paddot"
                if not os.path.exists(self.dir):
                    os.makedirs(self.dir, 0755)
                else:
                    print "Directory already exist"
            elif self.sistm == 'Darwin':
                try:
                    os.makedirs('~/Paddot')
                except OSError:
                    print "Directory already exist"
            elif self.sistm == 'Windows':
                try:
                    os.makedirs('C://')
                except OSError:
                    print "Directory already exist"
            self.sel = []
            self.parent = Tk()
            self.parent.title("Working directory")
            self.x = 0
            self.ste = IntVar(master=self.parent)
            self.arr = {}
            self.clustr = StringVar(master=self.parent)
            self.method = IntVar(master=self.parent)
            self.frametools = Frame(self.parent, height=200, width=300)
            self.frametools.pack(side=TOP, fill=BOTH, expand=True)
            # self.dat = data_m()
            self.pros = Pdb()
            # Second Frame
            self.scndfrm = Frame(self.parent, height=200, width=500)
            self.scndfrm.pack(side=BOTTOM, expand=True, fill="both")
    
            self.dlgframe = Frame(self.scndfrm, width=300, height=100)
            self.dlgframe.grid(column=0, row=0, sticky="nswe", padx=3, pady=3)
            self.cnv = Canvas(self.dlgframe, width=250, height=150)
            self.cnv.grid(row=0, column=0, sticky='nswe')
    
            self.hScroll = Scrollbar(self.dlgframe, orient=HORIZONTAL, command=self.cnv.xview)
            self.hScroll.grid(row=1, column=0, sticky='we')
            self.vScroll = Scrollbar(self.dlgframe, orient=VERTICAL, command=self.cnv.yview)
            self.vScroll.grid(row=0, column=1, sticky='ns')
            self.cnv.configure(xscrollcommand=self.hScroll.set, yscrollcommand=self.vScroll.set)
            self.frm = Frame(self.cnv, height=100)
            self.frm.pack(fill="both", expand=True)
            self.frm.pack_propagate(False)
            # # This puts the frame in the canvas's scrollable zone
            self.cnv.create_window(0, 0, window=self.frm, anchor='nw')
    
            self.openlabel = Label(self.frametools, text="Open Directory")
            self.openlabel.grid(row=1, column=0)
            self.browsebtn = Button(self.frametools, text="Browse",
                                    command=lambda: self.loadtemplate(self.cnv, self.frm, self.arr, self.parent), width=10)
            self.browsebtn.grid(row=1, column=1, sticky="sw", padx=2, pady=2)
            self.workdir = Label(self.frametools, text="Save to Working Directory")
            self.workdir.grid(row=3, column=0)
            self.folderbrs = Button(self.frametools, text="Browse", width=10,
                                    command=lambda: self.savedir())
            self.folderbrs.grid(row=3, column=1, sticky="sw", padx=2, pady=2)
            self.dlg_all = Checkbutton(self.scndfrm, text="Select all",
                                       command=lambda: self.checkbtn(self.ste, self.dlg_all), onvalue=1, offvalue=0,
                                       variable=self.ste)
            self.dlg_all.grid(row=2, column=0)
            self.clusfrm = Frame(self.scndfrm, width=100, height=120, bd=1, relief=SUNKEN)
            self.clusfrm.grid(row=0, column=2, sticky=N + S + W)
            self.clusfrm.grid_propagate(0)
            # clusfrm.grid_rowconfigure(1, weight= 2, minsize= 6)
    
            self.clslbl = Label(self.clusfrm, text="Clustering")
            self.clslbl.grid(row=0, column=0)
    
            self.eucrdbt = Radiobutton(self.clusfrm, text="Euclidian",
                                       variable=self.clustr, value="eucl", command='''lambda :self.clustr.set("eucl")''')
            self.eucrdbt.grid(row=1, column=0, sticky=W + N + S)
            self.eucrdbt.select()
    
            self.mngrdbt = Radiobutton(self.clusfrm, text="Manhattan", variable=self.clustr,
                                       value="manh", command=lambda: self.clustr.set("manh"))
            self.mngrdbt.grid(row=2, column=0, sticky=W + N + S)
            self.methframe = Frame(self.scndfrm, width=150, height=120, bd=1, relief=SUNKEN)
            self.methframe.grid(row=0, column=1, sticky=N + S)
            self.methframe.grid_propagate(0)
    
            self.mthlbl = Label(self.methframe, text="Method")
            self.mthlbl.grid(row=0, column=0, sticky=W + N + S)
            self.rmsdrb = Radiobutton(self.methframe, text="RSMD",
                                      variable=self.method, value=1)
            self.rmsdrb.grid(row=1, column=0, sticky=W + S + N)
            self.rmsdrb.select()
    
            self.avrgrb = Radiobutton(self.methframe, text="Average",
                                      variable=self.method, value=2)
            self.avrgrb.grid(row=2, column=0, sticky=W + N + S)
    
            self.comprb = Radiobutton(self.methframe, text="Complete",
                                      variable=self.method, value=3)
            self.comprb.grid(row=3, column=0, sticky=W + N + S)
    
            self.snglrb = Radiobutton(self.methframe, text="Single",
                                      variable=self.method, value=4)
            self.snglrb.grid(row=4, column=0, sticky=W + S + N)
    
            self.rmsdtxt = Entry(self.methframe, width=5)
            self.rmsdtxt.insert(2, "2.0")
            self.rmsdtxt.grid(row=1, column=1)
    
            self.cnclbt = Button(self.scndfrm, text="Cancel", width=10,
                                 command=lambda: self.cerrar(self.parent))
            self.cnclbt.grid(row=2, column=1, sticky=N + W)
    
            self.okbtn = Button(self.scndfrm, text="Ok", width=10, command=lambda: self.ok(self.clustr, self.parent,
                                                                                           self.rmsdtxt.get()))
            self.okbtn.grid(row=2, column=2, sticky=N + W)
    
        # print self.clustr.get()
        def plot(self, minn, maxx):
            self.fig = Figure(figsize=(4, 4), dpi=100)
            self.grad = self.fig.add_axes([0.05, 0.80, 0.9, 0.05])
            self.colr = mpl.cm.cool
            self.norm = mpl.colors.normalize(vmin=minn, vmax=maxx)
            cb1 = mpl.colorbar.ColorbarBase(self.grad, cmap=self.colr, norm=self.norm, orientation="horizontal")
            self.canvas = FigureCanvasTkAgg(self.fig, master=self.nw_root).show()
            self.canvas.get_tk_widget().pack(side=TOP, fill=BOTH, expand=1)
            return self.nw_root
    
        def loadtemplate(self, cnv, frme, arr, parent):
            self.parent = parent
            self.frm = frme
            self.cnv = cnv
            self.arr = arr
            self.selt = []
            global dirname
            try:
                self.dirname = tkFileDialog.askdirectory()
                os.chdir(self.dirname)
    
            except:
                pass
            self.cnt = 0
            # Lista donde guardaremos los nombres de los archivos .dlg
            for name in glob.glob('*.dlg'):
                self.arr[name] = IntVar(self.parent)  # Anadimos una clave al diccionario con el valor de 0
            for key in self.arr:
                # self.arr[key] = IntVar()#Cambiamos el valor de 0 por un IntVar para poder trabajar con el en tkinter
                self.r = Checkbutton(self.frm, text=key, onvalue=1, offvalue=0, variable=self.arr[key])
                self.selt.append(self.r)
                self.r.grid(row=self.cnt, column=1, sticky=W)
                self.cnt += 1
            self.frm.update_idletasks()
            # print self.arr
            # # Configure size of canvas's scrollable zone
            self.cnv.configure(scrollregion=(0, 0, self.frm.winfo_width(), self.frm.winfo_height()))
            self.frm.update_idletasks()
            # # Configure size of canvas's scrollable zone
            self.cnv.configure(scrollregion=(0, 0, self.frm.winfo_width(), self.frm.winfo_height()))
    
        def savedir(self):
            try:
                self.dirct = tkFileDialog.askdirectory()
                self.dirct += "/"
    
            except:
                self.dirct = self.dirname
                tkMessageBox.showinfo("Advertencia", "El trabajo se guardara en " + str(os.getcwd()))
    
        # return self.arr
        def checkbtn(self, ste, chkdlg):
            chkdlg.update_idletasks()
            if ste.get() == 1:
                for key, value in self.arr.items():
                    self.arr[key].set(1)
            if ste.get() == 0:
                for key, value in self.arr.items():
                    self.estado = value.get()
                    self.arr[key].set(0)
    
        def ok(self, clustr, parent, rmsd):
            self.m = {}
            # self.plt = grap(parent)
            parent.iconify()
            # self.scn_root = Tk()
            # self.frme = Frame(self.scn_root,width= 200, height= 200)
            # self.frme.pack(expand= False )
            try:
                self.menuBar.addmenu('PADDOT-plugin', 'Menu de PADDOT')
                self.menuBar.addcascademenu('PADDOT-plugin', 'PDB Files', 'Set some other preferences', traverseSpec='z',
                                            tearoff=0)
    
            except ValueError:
                tkMessageBox.showerror("Error", "Ya se creo el menu de PADDOT")
                parent.destroy()
            if clustr.get() == "eucl":
                for key, value in self.arr.items():
                    if self.arr[key].get() == 1:
                        self.pros.pross(key, self.dirct, rmsd)
                        try:
                            self.menuBar.addmenuitem('PDB Files', 'command', label=key.replace(".dlg", ".pdb"),
                                                     command=lambda i=key: self.visual(i))
                        except AttributeError:
                            tkMessageBox.showerror("Error", "The menu is already set")
            elif clustr.get() == "manh":
                tkMessageBox.showinfo("Opcion", "Manhattan")
    
                # self.fbemin, self.fbemax = self.pros.pross(key, self.dirname)
    
        def visual(self, uno):
            cmd.reinitialize()
            uno = uno.replace(".dlg", ".pdb")
            cmd.load(self.dirct + uno)
    
        @staticmethod
        def cerrar(parent):
            parent.destroy()
    
        def selec(self):
            pass
            #GUI()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
