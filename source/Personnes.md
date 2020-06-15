---
title: Personnes
date: 2020-05-07
---
Example Python program Personnes.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* # On importe Tkinter
* import Tkinter
* import sys
* import MySQLdb
* import string
* import tkMessageBox
* import re
* import time
* import multilistbox

## Methods

* def statistiques():
* def connexion():
* def formulaire():
* def ajout():
* def rechercher():
* def modification():
* def suppression():

## Code

Python tkinter example

    # On importe Tkinter
    import Tkinter
    import sys
    import MySQLdb
    import string
    import tkMessageBox
    import re
    import time
    import multilistbox
    
    # Nom du login pour la BDD
    global nom_log
    # MDP de la BDD
    global mdp_log
    
    # Données du formulaire
    global nom
    global prenom
    global mdp
    global societe
    global date_naissance
    global taille
    global Id
    global genre
    global filtre
    global fenetre2
    
    global db
    global cursor
    global i
    global j
    #Savoir si la BDD est déjà connectée
    global connexion_bdd
    global bouton_utilisateur
    global fenetre
    
    # Fonction du pogramme qui gère la connexion à la BDD
    def statistiques():
        global mlb
        global filtre
        
        fenetre3 = Tkinter.Toplevel()
        
        fenetre3.title("Statistiques")
    
        fenetre3.resizable(width=False,height=False)
    
        recherche = Tkinter.StringVar()
    
        nomlog_label = Tkinter.Label(fenetre3, text=nom_log.get())
        nomlog_bouton = Tkinter.Button(fenetre3, text = "Log off",command=fenetre3.destroy)
        recherche_bouton = Tkinter.Button(fenetre3, text = "Recherche", command = rechercher)
    
        filtrer_label = Tkinter.Label(fenetre3, text="Filtrer les noms")
        filtrer_entry = Tkinter.Entry(fenetre3, textvariable = filtre)
    
        tab_nom_label = Tkinter.Label(fenetre3, text="Nom")
        tab_prenom_label = Tkinter.Label(fenetre3, text="Prenom")
        tab_datenaiss_label = Tkinter.Label(fenetre3, text="DateNaissance")
        tab_societe_label = Tkinter.Label(fenetre3, text="Société")
        tab_taille_labal = Tkinter.Label(fenetre3, text="Taille")
        tab_sexe_label = Tkinter.Label(fenetre3, text="Sexe")
    
        modifier_bouton = Tkinter.Button(fenetre3, text="Modifier", command = modification )
        supprimer_bouton = Tkinter.Button(fenetre3, text="Supprimer", command = suppression)
    
        mlb = multilistbox.MultiListbox(fenetre3, (('Nom', 40), ('Prénom', 20), ('DateNaissance', 10), ('Société', 20), ('Taille', 5), ('Sexe', 5)))
    
        nomlog_label.grid(row = 0, column = 4)
        nomlog_bouton.grid(row = 0, column = 5)
        filtrer_label.grid(row=1, column=4)
        filtrer_entry.grid(row=1, column=5)
        recherche_bouton.grid(row=1, column=6)
        mlb.grid(row=3, column =0, columnspan=6)
        supprimer_bouton.grid(row = 4, column = 5)
    
        
        modifier_bouton.grid(row=4, column=6)
    
        Id=cursor.execute("SELECT Id FROM Personne")
        cursor.execute("SELECT LastName,FirstName,BirthDate,Company,Height,Gender FROM Personne ORDER BY LastName DESC, FirstName DESC" )
        Test=cursor.fetchall()
        for i in range (0,Id):
            mlb.insert(END,Test[i])
    
        fenetre3.mainloop()
    
    def connexion():
        global i
        global fenetre
        global bouton_utilisateur
        Id=cursor.execute("SELECT Id FROM Personne")
        
        for i in range (0,Id):
            cursor.execute("SELECT LastName FROM Personne")
            Nom = cursor.fetchall()
            cursor.execute("SELECT Password from Personne")
            Mdp = cursor.fetchall()
            if ((("%s" % Nom[i]) == nom_log.get()) and (("%s" % Mdp[i]) == mdp_log.get())):
                tkMessageBox.showinfo("Info","Connexion réussie")
                bouton_utilisateur = Tkinter.Button(fenetre, padx=10, pady=20, text="Nouvel utilisateur", command=formulaire)
                bouton_utilisateur.grid(row=1, column=2)
                statistiques()
                break
    
    # Fonction du programme qui gère le formulaire
    def formulaire():
        global fenetre2
        
        fenetre2 = Tkinter.Toplevel()
        
        fenetre2.title("Nouvel utilisateur")
    
        # L'on empêche de dérègler la fenêtre
        fenetre2.resizable(width=False,height=False)
    
    
        # Déclaration des widgets qui composent la fenêtre
        rien_label = Tkinter.Label(fenetre2, text="")
        
        completer_label = Tkinter.Label(fenetre2, text="Veuillez compléter : ")
        
        nom_label = Tkinter.Label(fenetre2, text="                   "+"Nom")
        nom_entry = Tkinter.Entry(fenetre2, textvariable=nom, text="" )
    
        prenom_label = Tkinter.Label(fenetre2, text="               "+"Prenom")
        prenom_entry = Tkinter.Entry(fenetre2, textvariable=prenom)
    
        mdp_label = Tkinter.Label(fenetre2, text="      "+"Mot de passe")
        mdp_entry = Tkinter.Entry(fenetre2, show="*", textvariable=mdp)
    
        societe_label = Tkinter.Label(fenetre2, text="              "+"Société")
        societe_entry = Tkinter.Entry(fenetre2, textvariable=societe)
    
        date_naissance_label = Tkinter.Label(fenetre2, text="Naissance (AAAA/MM/JJ)")
        date_entry = Tkinter.Entry(fenetre2, textvariable=date_naissance, width = 10)
    
        R1 = Tkinter.Radiobutton(fenetre2, text="homme", variable=genre, value=1)
        R2 = Tkinter.Radiobutton(fenetre2, text="femme", variable=genre, value=0)
    
        taille_label = Tkinter.Label(fenetre2, text="Taille (en cm)")
        taille_scale = Tkinter.Spinbox(fenetre2, from_=0, to=250, textvariable=taille)
    
        valider_bouton = Tkinter.Button(fenetre2, padx=50, pady=20, text="Valider", command=ajout)
    
        can2 = Tkinter.Canvas(fenetre2, width =110, height =90, bg ='white')
    
        photo2 = Tkinter.PhotoImage(file ='image2.gif')
        item2 = can2.create_image(77, 65, image =photo2)
    
        # Positionnement des composants dans la fenêtre
        can2.grid(row=0, column=1, rowspan=4)
        completer_label.grid(row=0, column=2)
        nom_label.grid(row=1, column=2)
        nom_entry.grid(row=1, column=3)
        prenom_label.grid(row=2, column=2)
        prenom_entry.grid(row=2, column=3)
        mdp_label.grid(row=3, column=2)
        mdp_entry.grid(row=3, column=3)
        societe_label.grid(row=4, column=2)
        societe_entry.grid(row=4, column=3)
        date_naissance_label.grid(row=1, column=4)
        date_entry.grid(row=1, column=5)
        
        R1.grid(row=2, column = 4)
        R2.grid(row=3, column = 4)
        taille_label.grid(row=4, column = 4)
        taille_scale.grid(row=4, column = 5)
        rien_label.grid(row=6, column = 1)
        valider_bouton.grid(row=7, column = 3)
        
        fenetre2.mainloop()
    
    
    # Fonction du programme qui gère l'inscertion des données dans la BDD
    def ajout():
        global nom
        global Id
        global fenetre2
        cursor = db.cursor()
        Id = cursor.execute("SELECT Id FROM Personne")
        
        # Expressions régulières pour tester si les données correspondent bien
        carac_num = re.compile('[0-9]')
        carac_lettres = re.compile('[a-zA-Z]')
        carac_spe = re.compile('[^a-zA-Z0-9_]')
        carac_nom = re.compile(' -')
        carac_naissance = re.compile('[0-9][0-9][0-9][0-9]/[ 01][0-9]/[ 0123][0-9]')
    
        # Test si les données entrées sont exactes
        try:
        
            if ((nom.get() == "") or (prenom.get() == "") or (date_naissance.get() == "") or (taille.get() == "") or (genre.get() == "")):
                tkMessageBox.showwarning("Attention", "Des champs sont vides !")
    
            elif ((carac_num.search(nom.get()) != None) or ((carac_spe.search(nom.get()) != None) and (carac_nom.search(nom.get()) != None ))):
                tkMessageBox.showwarning("Attention", "Des caractères ne correspondent pas dans le champ 'nom' !")
    
            elif ((carac_num.search(prenom.get()) != None) or ((carac_spe.search(prenom.get()) != None) and (carac_nom.search(prenom.get()) != None ))):
                tkMessageBox.showwarning("Attention", "Des caractères ne correspondent pas dans le champ 'prenom' !")
    
            elif ((carac_naissance.search(date_naissance.get()) == None)):
                tkMessageBox.showwarning("Attention", "Des caractères ne correspondent pas dans le champ 'naissance' !")
                
            # Test si l'on est bien connecté à la BDD
            elif (connexion_bdd == 0):
                tkMessageBox.showwarning("Attention", "Vous n'êtes pas connecté à la BDD !")
    
            else:
                Id=cursor.execute("SELECT Id FROM Personne")            
                cursor.execute ("INSERT INTO Personne (FirstName,LastName,BirthDate,Company,Height,Gender,Password ) VALUES(%s, %s,%s,%s,%s, %s, %s)", (prenom.get(), nom.get(), date_naissance.get(), societe.get(), taille.get(), genre.get(), mdp.get()))
                tkMessageBox.showinfo("Information", "Vos données ont bien été insérés dans la BDD !")
                db.commit()
    
        except Exception:
            tkMessageBox.showwarning("Attention", "Il y a eu une erreur de saisie dans un champ !")
            
            try:
                rechercher()
    
            except Exception:
                print "Fenetre statitiques non ouverte"
            
    
    # Fonction qui filtre les noms recherchés
    def rechercher():
        global i
        global filtre
        global j
    
        if(filtre.get()==""):
            mlb.delete(0,END)
            Id=cursor.execute("SELECT Id FROM Personne")
            cursor.execute("SELECT LastName,FirstName,BirthDate,Company,Height,Gender FROM Personne ORDER BY LastName DESC, FirstName DESC" )
            Test=cursor.fetchall()
            for i in range (0,Id):
                mlb.insert(END,Test[i])
                
        else:
            mlb.delete(0,END)
            Id=cursor.execute("SELECT Id FROM Personne")
            j=0
            for i in range (0,Id):
                cursor.execute("SELECT LastName FROM Personne")
                Nom = cursor.fetchall()    
                if ((("%s" % Nom[i]) == filtre.get())):            
                    cursor.execute("SELECT LastName,FirstName,BirthDate,Company,Height,Gender FROM Personne WHERE LastName like %s ORDER BY LastName DESC",Nom[i])  
                    Test=cursor.fetchall()
                    mlb.insert(ACTIVE,Test[j])
                    j=j+1
    
    def modification():
        suppression()
        formulaire() 
    
    
    def suppression():
        
        index = mlb.curselection()
        ligne = mlb.get(index)
        ligne_donnees = list(ligne)
        cursor.execute("SELECT COUNT(*) FROM Personne")
        nb = cursor.fetchall()
        # Conversion du nombre de données dans la base en int
        nb = str('.'.join(str(x) for x in nb))
        nb = nb[1:-3]
        nb = int(nb)
        # Suppression de la ligne dans la base de données
        try:
            for i in range (0, nb):
                cursor.execute("SELECT LastName FROM Personne")
                Nom = cursor.fetchall()
                cursor.execute("SELECT FirstName FROM Personne")
                Prenom = cursor.fetchall()
                cursor.execute("SELECT BirthDate FROM Personne")
                Anniv = cursor.fetchall()
                if ((("%s" % Nom[i]) == ligne_donnees[0]) and (("%s" % Prenom[i]) == ligne_donnees[1]) and (("%s" % Anniv[i]) == ligne_donnees[2])):
                    cursor.execute("DELETE FROM Personne WHERE  FirstName=%s AND LastName=%s AND  BirthDate=%s ",(ligne_donnees[1],ligne_donnees[0],ligne_donnees[2]))
                    db.commit()
                    rechercher()
        except Exception:
            nb = nb-1
                
    #Fenêtre principale du programme
    
    # On crée une fenêtre, racine de notre interface
    fenetre = Tkinter.Tk()
    
    fenetre.title("Accueil")
    
    # L'on empêche de dérègler la fenêtre
    fenetre.resizable(width=False,height=False)
    
    # Déclaration des variables globales qui contiennent les données entrées dans les Entry
    nom = Tkinter.StringVar()
    prenom = Tkinter.StringVar()
    mdp = Tkinter.StringVar()
    societe = Tkinter.StringVar()
    date_naissance = Tkinter.StringVar()
    taille = Tkinter.IntVar()
    genre = Tkinter.StringVar()
    filtre = Tkinter.StringVar()
    Id = Tkinter.IntVar()
    nom_log = Tkinter.StringVar()
    mdp_log = Tkinter.StringVar()
    j=0
    
    # Déclaration de la BDD non connecté à l'origine
    connexion_bdd = 0
    
    # Déclaration des widgets qui composent la fenêtre Déclaration
    nom_label = Tkinter.Label(fenetre, text="                           "+"Nom")
    nom_entry = Tkinter.Entry(fenetre, textvariable=nom_log, width = 20)
    
    mdp_label = Tkinter.Label(fenetre, text="               "+"Mot de passe") 
    mdp_entry = Tkinter.Entry(fenetre, show="*", textvariable=mdp_log, width = 20)
    
    entrer_bouton = Tkinter.Button(fenetre, padx=20, pady=10, text="Entrer", command=connexion)
    
    identification_label = Tkinter.Label(fenetre, text="Veuillez vous identifier : ") 
    
    bouton_utilisateur= Tkinter.Button(fenetre, padx=10, pady=20, text="Nouvel utilisateur", state=DISABLED, command=formulaire)
    
    bouton_quit= Tkinter.Button(fenetre,padx=30, pady=20, text="Quitter",  command=fenetre.destroy)
    
    can1 = Tkinter.Canvas(fenetre, width =160, height =130, bg ='white')
    photo = Tkinter.PhotoImage(file ='image.gif')
    item = can1.create_image(80, 70, image =photo)
    
    # Positionnement des composants dans la fenêtre
    can1.grid(row =1, column =0)
    identification_label.grid(row=2, column=0)
    nom_label.grid(row=4, column=0)
    nom_entry.grid(row=4, column=1)
    mdp_label.grid(row=5, column=0)
    mdp_entry.grid(row=5, column=1)
    entrer_bouton.grid(row=4, column=2, rowspan=2)
    bouton_utilisateur.grid(row=1, column=2)
    bouton_quit.grid(row=8, column=1)
    
        # On vérifie que l'on est pas déjà connecté à la BDD
    if (connexion_bdd == 1):
        tkMessageBox.showwarning("Attention", "La BDD est déjà connectée !")
    
    # Si l'on est pas connectés on se connectes si les login et mdp sont bien exactes
    else:
        try:
            db = MySQLdb.connect(host = "localhost",user = "root", passwd = "iutgeii",db='Informations')
              
        except:
            tkMessageBox.showwarning("Attention", "Connexion BDD échouée !")
            raise
    
        tkMessageBox.showinfo("Information", "Connexion BDD réussie !")
        connexion_bdd = 1 
        cursor = db.cursor()
        db.commit()  
    # On démarre la boucle Tkinter qui s'interompt quand on ferme la fenêtre
    fenetre.mainloop()
    db.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
