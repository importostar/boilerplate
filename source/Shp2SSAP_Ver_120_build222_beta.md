---
title: Shp2SSAP_Ver_120_build222_beta
date: 2020-05-07
---
Example Python program Shp2SSAP_Ver_120_build222_beta.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* import linecache
* import Shp2SSAP_Ver_120_build220_beta_MainFunc as FuncMain
* import xy2shp_forSSAP_Ver_120_build220_beta_XYFunc as FuncXY
* import tkinter.filedialog
* from tkinter import *
* from tkinter import ttk
* import s2s_lbl_ver120_build220 as s2s_lbl

## Classes

* class Shp2SSAP_GUI(object):

## Methods

* def __init__(self, parent):
* def load_shapefile(self):
* def save_files_ssap(self):
* def active_disable_button(self, *args):
* def openSubFormXY(self):
* def load_textfile(self):
* def load_clipboard(self):
* def save_shapefile(self):
* def onCloseOtherFrame(self, otherFrame):
* def show(self):

## Code

Python tkinter example

    # ver 120 - build 222
    # Prima versione con Classe dedicata all'interfaccia e richiamo delle funzioni da modulo esterno
    # Stack delle finestre non ottimale: non riesco a mantenere in primo piano la finestra secondaria
    
    # exit button: risolto funziona (self.root.destroy)
    import sys
    
    sys.path.insert(0, '../moduli_py')
    import os
    import linecache
    import Shp2SSAP_Ver_120_build220_beta_MainFunc as FuncMain
    import xy2shp_forSSAP_Ver_120_build220_beta_XYFunc as FuncXY
    import tkinter.filedialog
    from tkinter import *
    from tkinter import ttk
    import s2s_lbl_ver120_build220 as s2s_lbl
    
    
    ########################################################################
    # Classe principale per la gestione dell'interfaccia
    # riporta le funzioni che pescano direttamente dalle variabili definite tramite interfaccia
    # Le altre funzioni sono definite nei moduli esterni Shp2SSAP_Ver_XXX_buildXXX_MainFunc
    # e xy2shp_forSSAP_Ver_XXX_buildXXX_XYFunc
    
    class Shp2SSAP_GUI(object):
        """
        # Classe principale per la gestione dell'interfaccia di Shp2SSAP
        # riporta le funzioni che pescano direttamente dalle variabili definite tramite interfaccia
        # Le altre funzioni sono definite nei moduli esterni Shp2SSAP_Ver_XXX_buildXXX_MainFunc
        # e xy2shp_forSSAP_Ver_XXX_buildXXX_XYFunc
    
        """
    
        # ----------------------------------------------------------------------
        def __init__(self, parent):
            """Constructor"""
            self.root = parent
            self.root.title(s2s_lbl.root_title)
            self.root.resizable(False, False)
            if os.path.exists('.\\Icon\\Shp2SSAP.ico'):
                self.root.iconbitmap('.\\Icon\\Shp2SSAP.ico')
            elif os.path.exists('Shp2SSAP.ico'):
                self.root.iconbitmap('Shp2SSAP.ico')
            else:
                pass
    
            self.frame = ttk.Frame(parent, padding="12 12 12 12")
            self.frame.grid(column=0, row=0, sticky=(N, W, E, S))
            self.frame.columnconfigure(0, weight=1)
            self.frame.rowconfigure(0, weight=1)
            self.frame['borderwidth'] = 2
            self.frame['relief'] = 'sunken'
    
            # Input box
            self.var1 = StringVar(self.root)
            self.var2 = StringVar(self.root)
            self.str_path_shape = Entry(self.frame, width=75, textvariable=self.var1)
            self.str_path_ssap = Entry(self.frame, width=75, textvariable=self.var2)
            self.str_path_shape.grid(row=2, column=1, sticky=(E, W))
            self.str_path_ssap.grid(row=3, column=1, sticky=(E, W))
            self.var1.trace("w", self.active_disable_button)
            self.var2.trace("w", self.active_disable_button)
    
            # checkbutton
            self.check_cu = IntVar()
            self.check_top_bottom_order = IntVar()
            self.c1 = Checkbutton(self.frame, text="Verifica ordinamento verticale strati",
                                  variable=self.check_top_bottom_order,
                                  onvalue=1, offvalue=0, height=1, width=35, anchor=W)
            self.c1.grid(row=5, column=0, sticky=W)
            self.c1.select()
            self.check_trimming = IntVar()
            self.c2 = Checkbutton(self.frame, text="Regola gli strati alla superficie topografica",
                                  variable=self.check_trimming,
                                  onvalue=1, offvalue=0, height=1, width=35, anchor=E)
            self.c2.grid(row=5, column=1, sticky=W)
            self.c2.select()
            self.check_smp_polyline = IntVar()
            self.c3 = Checkbutton(self.frame, text="Semplifica polyline se > 100 punti", variable=self.check_smp_polyline,
                                  onvalue=1, offvalue=0, height=1, width=35, anchor=W)
            self.c3.grid(row=6, column=0, sticky=W)
            self.c3.select()
    
            # BUTTONS
            self.XY_Button = Button(self.frame, text='Crea Shape da XY', command=self.openSubFormXY)
            self.XY_Button.grid(row=1, column=0, sticky=(W, E), pady=4, padx=8)
            self.In_Button = Button(self.frame, text='Input Shapefile', command=self.load_shapefile)
            self.In_Button.grid(row=2, column=0, sticky=(W, E), pady=4, padx=8)
            self.Out_Button = Button(self.frame, text='Output SSAP files', command=self.save_files_ssap)
            self.Out_Button.grid(row=3, column=0, sticky=(W, E), pady=4, padx=8)
            self.Exit_Button = Button(self.frame, text='Esci', command=self.root.destroy)
            self.Exit_Button.grid(row=8, column=1, sticky=E, pady=4)
            self.Ver_Button = Button(self.frame, text='Verifica preliminare Shape', command=lambda:
            FuncMain.check_function(1, self.str_path_shape, self.check_top_bottom_order.get(),
                                    self.check_smp_polyline.get()))
            self.Ver_Button.grid(row=8, column=0, sticky=W, pady=4)
            self.Conv_Button = Button(self.frame, text='Converti', command=lambda:
            FuncMain.shp_2_ssap_files(self.str_path_shape, self.str_path_ssap, self.check_top_bottom_order.get(),
                                      self.check_trimming.get(), self.check_smp_polyline.get()))
            self.Conv_Button.grid(row=8, column=0, sticky=E, pady=4)
            self.Conv_Button.configure(state=DISABLED)
            self.Ver_Button.configure(state=DISABLED)
    
            # Separator
            s1 = ttk.Separator(self.frame, orient=HORIZONTAL).grid(column=1, row=1, sticky=(E, W), pady=6)
            s2 = ttk.Separator(self.frame, orient=HORIZONTAL).grid(column=1, row=4, sticky=(E, W), pady=6)
            s3 = ttk.Separator(self.frame, orient=HORIZONTAL).grid(column=0, row=7, sticky=(E, W), pady=10, columnspan=3)
    
            # label
            l1 = ttk.Label(self.frame, text='  Opzioni controllo e creazioni strati', borderwidth=5, relief=GROOVE,
                           foreground='black')
            l1.grid(column=0, row=4, pady=10, ipadx=10, ipady=3, sticky=(E, W))
    
        def load_shapefile(self):
            """
            Funzione di caricamento degli sahpefile di input.
            Funzione richiamata dall'interfaccia
            """
            # load default path value from default.txt file
            self.defpathshp = os.getcwd() + linecache.getline("default.txt", 2)
            self.defpathshp = self.defpathshp[:-1]  # remove /n special character
            self.str_path_shape.delete(0, END)
            if os.path.exists(self.defpathshp) == False:
                self.defpathshp = ""
            self.shp_name = tkinter.filedialog.askopenfilename(filetypes=(("Shapefile", "*.shp"), ("All files", "*.*")),
                                                               initialdir=self.defpathshp)
            self.str_path_shape.insert(10, self.shp_name)
            linecache.clearcache()
    
        def save_files_ssap(self):
            """
            Funzione di definzione dei file SSAP di output.
            Funzione richiamata dall'interfaccia tkinter
            """
            self.defpathssap = os.getcwd() + linecache.getline("default.txt", 4)
            self.defpathssap = self.defpathssap[:-1]  # remove /n special character
            self.str_path_ssap.delete(0, END)
            if not os.path.exists(self.defpathssap):
                self.defpathssap = ""
            self.SSAP_name = tkinter.filedialog.asksaveasfilename(
                filetypes=(("SSAP FILES", "*.mod*"), ("All files", "*.*")),
                initialdir=self.defpathssap)
            self.ssap_text_pathname = os.path.splitext(self.SSAP_name)[0]
            self.str_path_ssap.insert(10, self.ssap_text_pathname)
            linecache.clearcache()
    
        def active_disable_button(self, *args):
            """
            active or disable button 'Converti' and 'Verifica' by input and output entry
            """
            x = self.var1.get()
            y = self.var2.get()
            z = self.SubForm.var_str_input.get()
            w = self.SubForm.var_str_output.get()
    
            if os.path.exists(x):
                self.Ver_Button.configure(state='normal')
            else:
                self.Conv_Button.configure(state='disabled')
                self.Ver_Button.configure(state='disabled')
            if os.path.isdir(os.path.dirname(y)) and os.path.basename(y) and os.path.exists(x):
                self.Conv_Button.configure(state='normal')
            else:
                self.Conv_Button.configure(state='disabled')
    
            if os.path.exists(z) == TRUE or z == FuncXY.msg_clipboard:
                if os.path.isdir(os.path.dirname(w)) and os.path.basename(w):
                    self.SubForm.ConvXY_Button.configure(state='normal')
            else:
                self.SubForm.ConvXY_Button.configure(state='disabled')
    
        # ----------------------------------------------------------------------
        def openSubFormXY(self):
            """"""
    
            # to check if windows is just opne:
            # if (self.SubForm is not None) and self.SubForm.winfo_exists():
            #     print('Window 2 exists')
            # else:
            #     print('Window 2 not exists')
            self.SubForm = Toplevel(self.root)
            self.SubForm.resizable(FALSE,FALSE)
            self.SubForm.title(s2s_lbl.subform_title + s2s_lbl.subform_ver)
    
            if os.path.exists('.\\Icon\\xy2Shp_forSSAP.ico'):
                self.SubForm.iconbitmap('.\\Icon\\xy2Shp_forSSAP.ico')
            elif os.path.exists('xy2Shp_forSSAP.ico'):
                self.SubForm.iconbitmap('xy2Shp_forSSAP.ico')
            else:
                pass
            self.frame = ttk.Frame(self.SubForm, padding="12 12 12 12")
            self.frame.grid(column=0, row=0, sticky=(N, W, E, S))
            self.frame.columnconfigure(0, weight=1)
            self.frame.rowconfigure(0, weight=1)
            self.frame['borderwidth'] = 2
            self.frame['relief'] = 'sunken'
    
            # Input box for input text file and output shapefile
            self.SubForm.var_str_input = tkinter.StringVar(self.SubForm)
            self.SubForm.path_txt_inputbox = tkinter.Entry(self.frame, width=70, textvariable=self.SubForm.var_str_input)
            self.SubForm.path_txt_inputbox.grid(row=0, column=1, sticky=(E, W), columnspan=1)
            self.SubForm.var_str_input.trace("w", self.active_disable_button)
    
            self.SubForm.var_str_output = tkinter.StringVar(self.SubForm)
            self.SubForm.strXY_path_shape = tkinter.Entry(self.frame, width=70, textvariable=self.SubForm.var_str_output)
            self.SubForm.strXY_path_shape.grid(row=1, column=1, sticky=(E, W), columnspan=1)
            self.SubForm.var_str_output.trace("w", self.active_disable_button)
    
            # checkbutton and input box for parameters value
            width_cb = 30
            self.check_phi = IntVar()
            self.c1 = Checkbutton(self.frame, text="Angolo d'attrito", variable=self.check_phi, onvalue=1,
                             offvalue=0, height=1, width=width_cb, anchor=W)
            self.c1.grid(row=4, column=0, sticky=W, padx=0, pady=0)
            self.c1.deselect()
            #check_phi.trace("w", active_disable_str_phi)
    
            self.var_phi = tkinter.DoubleVar(self.SubForm)
            self.str_phi = tkinter.Entry(self.frame, width=5, textvariable=self.var_phi, state=DISABLED)
            self.str_phi.grid(row=4, column=0, sticky=E, padx=0, pady=0)
            self.var_phi.set(FuncXY.default_phi)
    
            self.check_c = IntVar()
            self.c2 = Checkbutton(self.frame, text="Coesione drenata (Kpa)", variable=self.check_c, onvalue=1,
                             offvalue=0, height=1, width=width_cb, anchor=W)
            self.c2.grid(row=5, column=0, sticky=W, padx=0)
            self.c2.deselect()
            #check_c.trace("w", active_disable_str_c)
    
            self.var_c = tkinter.DoubleVar(self.SubForm)
            self.str_c = tkinter.Entry(self.frame, width=5, textvariable=self.var_c, state=DISABLED)
            self.str_c.grid(row=5, column=0, sticky=E)
            self.var_c.set(FuncXY.default_c)
    
            self.check_cu = IntVar()
            self.c3 = Checkbutton(self.frame, text="Coesione non drenata (Kpa)", variable=self.check_cu, onvalue=1,
                             offvalue=0, height=1, width=width_cb, anchor=W)
            self.c3.grid(row=6, column=0, sticky=W, padx=0)
            self.c3.deselect()
            #check_cu.trace("w", active_disable_str_cu)
    
            self.var_cu = tkinter.DoubleVar(self.SubForm)
            self.str_cu = tkinter.Entry(self.frame, width=5, textvariable=self.var_cu, state=DISABLED)
            self.str_cu.grid(row=6, column=0, sticky=E)
            self.var_cu.set(FuncXY.default_cu)
    
            self.check_gamma = IntVar()
            self.c4 = Checkbutton(self.frame, text="Peso di volume naturale (KN/mc):", variable=self.check_gamma, onvalue=1,
                             offvalue=0, height=1, width=width_cb, anchor=W)
            self.c4.grid(row=4, column=1, sticky=W, padx=30)
            self.c4.deselect()
    
            #check_gamma.trace("w", active_disable_str_gamma)
    
            self.var_gamma = tkinter.DoubleVar(self.SubForm)
            self.str_gamma = tkinter.Entry(self.frame, width=5, textvariable=self.var_gamma, state=DISABLED)
            self.str_gamma.grid(row=4, column=1, sticky=E, padx=100)
            self.var_gamma.set(FuncXY.default_gamma)
    
            self.check_gammasat = IntVar()
            self.c5 = Checkbutton(self.frame, text="Peso di volume saturo (KN/mc):", variable=self.check_gammasat, onvalue=1,
                             offvalue=0, height=1, width=width_cb, anchor=W)
            self.c5.grid(row=5, column=1, sticky=W, padx=30)
            self.c5.deselect()
    
    
            #check_gammasat.trace("w", active_disable_str_gammasat)
            self.var_gammasat = tkinter.DoubleVar(self.SubForm)
            self.str_gammasat = tkinter.Entry(self.frame, width=5, textvariable=self.var_gammasat, state=DISABLED)
            self.str_gammasat.grid(row=5, column=1, sticky=E, padx=100)
            self.var_gammasat.set(FuncXY.default_gammasat)
    
            #button
            self.SubForm.ButtonInputXY = Button(self.frame, text='Input file di testo', command=self.load_textfile)
            self.SubForm.ButtonInputXY.grid(row=0, column=0, sticky=(W), pady=4, padx=8)
            self.SubForm.ButtonInputClipBoard = Button(self.frame, text='Input appunti', command=self.load_clipboard)
            self.SubForm.ButtonInputClipBoard.grid(row=0, column=0, sticky=(E), pady=4, padx=8)
            self.SubForm.ButtonOutputShp = Button(self.frame, text='Output Shapefile per SSAP', command=self.save_shapefile)
            self.SubForm.ButtonOutputShp.grid(row=1, column=0, sticky=(W, E),
                                                                                          pady=4, padx=8)
    
            self.SubForm.ConvXY_Button = Button(self.frame, text='Converti', command=FuncXY.convert_txt2shp)
            self.SubForm.ConvXY_Button.grid(row=14, column=0, sticky=W, pady=4)
            self.SubForm.ConvXY_Button.configure(state=DISABLED)
            self.SubForm.ExitXY_Button = Button(self.frame, text='Esci', command=self.SubForm.destroy)
            self.SubForm.ExitXY_Button.grid(row=14, column=1, sticky=E, pady=4)
    
            # separator
            s1_0 = ttk.Separator(self.frame, orient=HORIZONTAL).grid(column=1, row=3, sticky=(E, W), pady=10, columnspan=2)
            s2_0 = ttk.Separator(self.frame, orient=HORIZONTAL).grid(column=0, row=9, sticky=(E, W), pady=10, columnspan=3)
            s3_0 = ttk.Separator(self.frame, orient=HORIZONTAL).grid(column=0, row=13, sticky=(E, W), pady=10, columnspan=3)
    
            # label
            l1 = ttk.Label(self.frame, text='                  Assegna valori a strato', borderwidth=5, relief=GROOVE,
                           foreground='black')
            l1.grid(column=0, row=3, pady=10, ipadx=5, ipady=3, sticky=(W, E))
    
            check_falda = IntVar()
            c6 = Checkbutton(self.frame, text="Superficie di saturazione parallela alla topografia a profondità di metri:",
                             variable=check_falda, onvalue=1,
                             offvalue=0, height=1, width=60, anchor=W)
            c6.grid(row=10, column=0, sticky=W, columnspan=2)
            c6.deselect()
    
            self.var_falda = tkinter.DoubleVar(self.SubForm)
            self.str_falda = tkinter.Entry(self.frame, width=5, textvariable=self.var_falda, state=DISABLED)
            self.str_falda.grid(row=10, column=1, sticky=E)
            self.var_falda.set(FuncXY.default_falda_deep)
    
            #check_falda.trace("w", active_disable_str_falda)
    
            check_pendenza_media = IntVar()
            c7 = Checkbutton(self.frame,
                             text="Angolo d'attrito = pendenza media pendio e coesione = 0 kpa (back analysis condizioni residue)",
                             variable=check_pendenza_media, onvalue=1,
                             offvalue=0, height=1, width=80, anchor=W)
            c7.grid(row=11, column=0, sticky=W, columnspan=2)
            c7.deselect()
    
            #check_pendenza_media.trace("w", active_disable_chkb_backanalysis)
            #check_phi.trace("w", active_disable_chkb_backanalysis)
            #check_c.trace("w", active_disable_chkb_backanalysis)
    
            check_bedrock = IntVar()
            c8 = Checkbutton(self.frame,
                             text="Substrato con resistenza infinita parallelo alla topografia  a profondità di metri:",
                             variable=check_bedrock, onvalue=1,
                             offvalue=0, height=1, width=60, anchor=W)
            c8.grid(row=12, column=0, sticky=W, columnspan=2)
            c8.deselect()
    
            var_bedrock = tkinter.DoubleVar(self.SubForm)
            str_bedrock = tkinter.Entry(self.frame, width=5, textvariable=var_bedrock, state=DISABLED)
            str_bedrock.grid(row=12, column=1, sticky=E)
            #var_bedrock.set(default_deep_bedrock)
    
            #check_bedrock.trace("w", active_disable_str_bedrock)
    
        # ----------------------------------------------------------------------
        def load_textfile(self):
            """
            Funzione di caricamento file di testo di input.
            Funzione richiamata dall'interfaccia
            """
            
            # load default path value from default.txt file
            self.SubForm.path_txt_inputbox.configure(state=NORMAL)
            default_path_txt = os.getcwd() + linecache.getline("default.txt", 10)
            default_path_txt = default_path_txt[:-1]  # remove /n special character
            self.SubForm.path_txt_inputbox.delete(0, END)  # pulisco il campo di input
            if os.path.exists(default_path_txt) == False:
                default_path_txt = ""
    
            #questo passaggio determina il foicsu sulla finestra root/parent non so il perchè        
            txt_filename = tkinter.filedialog.askopenfilename(filetypes=(("txt file", "*.txt"), ("All files", "*.*")),
                                                              initialdir=default_path_txt)
            self.SubForm.focus()# richiamo in primo piano la finestra SubForm - non è perfetto
            self.SubForm.path_txt_inputbox.insert(10, txt_filename)
            linecache.clearcache()
        # ----------------------------------------------------------------------
        def load_clipboard(self):
            try:
                self.SubForm.path_txt_inputbox.delete(0, END)  # pulisco il campo di input
                self.SubForm.path_txt_inputbox.insert(10, FuncXY.msg_clipboard)
                self.SubForm.path_txt_inputbox.configure(state=DISABLED)
            except:
                pass
        # ----------------------------------------------------------------------
        def save_shapefile(self):
            """
            Funzione di definzione dei file SSAP di output.
            Funzione richiamata dall'interfaccia tkinter
            """
            try:
                if os.access("default.txt", os.F_OK):
                    defpathshape = os.getcwd() + linecache.getline("default.txt", 2)
                    defpathshape = defpathshape[:-1]  # remove /n special character
                    self.SubForm.strXY_path_shape.delete(0, END)
                SHP_name = tkinter.filedialog.asksaveasfilename(filetypes=(("Shapefile", ".shp"), ("All files", "*.*")),
                                                                initialdir=FuncXY.defpathshape)
                self.SubForm.focus()  # richiamo in primo piano la finestra SubForm - non è perfetto
                if SHP_name.split(".")[-1] == "shp":
                    self.SubForm.strXY_path_shape.insert(10, SHP_name)
                else:
                    self.SubForm.strXY_path_shape.insert(10, SHP_name + ".shp")
                linecache.clearcache()
            except:
                pass
        # ----------------------------------------------------------------------
    
        def onCloseOtherFrame(self, otherFrame):
            """"""
            otherFrame.destroy()
            # self.show()
    
        # ----------------------------------------------------------------------
        def show(self):
            """"""
            self.root.update()
            self.root.deiconify()
    
    
    # ----------------------------------------------------------------------
    if __name__ == "__main__":
        root = Tk()
        app = Shp2SSAP_GUI(root)
        root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
