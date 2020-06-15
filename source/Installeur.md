---
title: Installeur
date: 2020-05-07
---
Example Python program Installeur.py

## Modules

* import urllib.request
* import os
* from tkinter import *
* from tkinter.filedialog import *
* from Tkinter import *
* from Tkinter.filedialig import *

## Methods

* def fermer():
* def ch_path():
* def install():

## Code

Python tkinter example

    #####################################
    #By AR2000                          #
    #Installation tool                  #
    #Download file directly on the web  #
    #####################################
    #IMPORTATION DES LIBRAIRIES=======================
    import urllib.request
    import os
    try:
        from tkinter import *
        from tkinter.filedialog import *
    except ImportError:
        from Tkinter import *
        from Tkinter.filedialig import *
    #=================================================
    NAME=""#Nom de l'installeur facultatif
    #=================================================
    global stop,path,fen,file_list
    file_list_web=""#Utiliser un fichier sur internet au lieu de fichier list.txt
    file_list=[]#Indiquer les fichier à télécharger sous forme d'une list double [[url,name],[url,name],...] au lieu de fichier list.txt
    stop=False
    fen = Tk()
    fen.title(NAME+" Installateur")
    path = StringVar(fen,value=os.getcwd())
    #=================================================
    def fermer():
        global stop
        stop=True
    
    def ch_path():
        global path,fen
        path.set(askdirectory(parent=fen,initialdir=os.getcwd(),mustexist=True,title="Installer dans :"))
        if path.get()=="":
            path.set(os.getcwd())
    
    def install():
        global file_list,path,fen
        text=StringVar()
        output=Message(fen,textvariable=text,bg="white",aspect=300,width=700,relief=RIDGE,bd=5)
        output.grid(row=1,column=0)
        b_cancel.configure(state=DISABLED)
        b_ok.configure(state=DISABLED)
        b_changer.configure(state=DISABLED)
        fen.update_idletasks()
    
        try:
            if file_list_web != "":#Depuis un fichier sur internet
                file = urllib.request.urlopen(file_list_web)
                while True:
                    line=str(file.readline().strip())[2:-1]
                    if line != "":
                        element=line.split(";")
                        if element[0]== "MKDIR":
                            try:
                                os.mkdir(path.get()+"/"+element[1].strip())
                                text.set(str(text.get().split("\n")[0:10]).replace("[","").replace("]","").replace("'","").replace(", ","\n")+"mkdir : "+element[1].strip()+"\n")
                                fen.update_idletasks()
                            except FileExistsError:
                                pass
                        else:
                            text.set(str(text.get().split("\n")[0:10]).replace("[","").replace("]","").replace("'","").replace(", ","\n")+"Donload "+element[0]+" as "+element[1]+"\n")
                            fen.update_idletasks()
                            urllib.request.urlretrieve(element[0],path.get()+"/"+element[1])
                    else:
                        break
                text.set(text.get()+"Terminé") 
                b_cancel.configure(state=NORMAL,text="Fermer")
                fen.update_idletasks()
                
            elif file_list != []:#Depuis la liste
                for element in file_list:
                    if element[0]== "MKDIR":
                        try:
                            os.mkdir(path.get()+"/"+element[1].strip())
                            text.set(str(text.get().split("\n")[0:10]).replace("[","").replace("]","").replace("'","").replace(", ","\n")+"mkdir : "+element[1].strip()+"\n")
                            fen.update_idletasks()
                        except FileExistsError:
                            pass
                    else:
                        text.set(str(text.get().split("\n")[0:10]).replace("[","").replace("]","").replace("'","").replace(", ","\n")+"Download "+element[0]+" as "+element[1]+"\n")
                        fen.update_idletasks()
                        urllib.request.urlretrieve(element[0],path.get()+"/"+element[1])
                text.set(text.get()+"Terminé")
                b_cancel.configure(state=NORMAL,text="Fermer")
                fen.update_idletasks()
                
            elif os.path.exists("list.txt") and os.path.isfile("list.txt"):#Avec le fichier list.txt
                with open("list.txt","r") as file:
                    for content in file:
                        element=content.strip().split(";")
                        if element[0]== "MKDIR":
                            try:
                                os.mkdir(path.get()+"/"+element[1].strip())
                                text.set(str(text.get().split("\n")[0:10]).replace("[","").replace("]","").replace("'","").replace(", ","\n")+"mkdir : "+element[1].strip()+"\n")
                                fen.update_idletasks()
                            except FileExistsError:
                                pass
                        else:
                            text.set(str(text.get().split("\n")[0:10]).replace("[","").replace("]","").replace("'","").replace(", ","\n")+"Donload "+element[0]+" as "+element[1]+"\n")
                            fen.update_idletasks()
                            urllib.request.urlretrieve(element[0],path.get()+"/"+element[1])
                text.set(text.get()+"Terminé")
                b_cancel.configure(state=NORMAL,text="Fermer")
                fen.update_idletasks()
            else:
                text.set("Error : nothing to install")
                fen.update_idletasks()
        except urllib.error.HTTPError:
            text.set(text.get()+"Erreur 404")
            b_cancel.configure(state=NORMAL,text="Fermer")
            fen.update_idletasks()
    #=================================================
    fen.protocol("WM_DELETE_WINDOW", fermer)
    t_frame = Frame(fen)
    text      =Label(t_frame,text="Installer dans : ")
    path_l    =Label(t_frame,textvariable=path,bg="white")
    b_changer =Button(t_frame,text="...",command=ch_path)
    text.grid(row=0,column=0)
    path_l.grid(row=0,column=1)
    b_changer.grid(row=0,column=2)
    t_frame.grid(row=0,column=0)
    
    b_frame = Frame(fen)
    b_ok      =Button(b_frame,text="INSTALLER",command=install)
    b_cancel  =Button(b_frame,text="ANNULER",command=fermer)
    b_ok.grid(row=0,column=0)
    b_cancel.grid(row=0,column=1)
    b_frame.grid(row=2,column=0)
    
    while stop==False:#Remplace le fen.mainloop()
        fen.update()  #Permet de garder plus de controle sur l'execution
    
    fen.destroy()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
