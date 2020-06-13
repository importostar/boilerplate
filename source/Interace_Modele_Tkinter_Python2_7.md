---
title: Interace_Modele_Tkinter_Python2_7
date: 2020-05-07
---
Example Python program Interace_Modele_Tkinter_Python2_7.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os   #Blibliotheque permettant l'interaction avec le systeme
* import sys  #Blibliotheque permettant l'interaction avec le systeme
* import datetime #Blibliotheque permettant d'obtenir la date
* import time #Blibliotheque permettant d'obtenir la date
* import getpass  #On importe la blibliotheque "getpass"
* from Tkinter import * #Python Version 2 #Blibliotheque permettant d'obtenir Tkinter(G.U.I)
* import ttk  #Blibliotheque permettant de charger un composant Tkinter(G.U.I)
* from nettoyage_du_cache import clear_cache  #Bibliotheque permettant de nettoyer les fichiers cache PYTHON
* from Infos_Hardware import CPU_usage#Obtention de l'utilisation du Processeur par le Systeme d'exploitation et ses programmes autour
* from Infos_Hardware import CPU_temp #Obtention de la Temperature du Processeur sur la carte mere
* from Infos_Hardware import SoC_info #Obtention des informations concernant le package CPU+GPU
* from Infos_Hardware import MEM_info #Obtention de l'utilisation de la Memoire Vive du Systeme

## Methods

* def temps_actuel():   
* def update_temps_actuel():  #Fonctionnalité permettant de mettre à jour l'Heure en fonction du Temps Réel
* def information_Materiel():
* def update_information_Materiel():
* def information_Complementaire():
* #def update_information_Complementaire():

## Code

Python tkinter example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    #AIDES: https://github.com/Franck1333/ProjetBrassard
    #AIDES: https://gist.github.com/Franck1333/f80936044088cb50aec1c1aad9de1803
    #AIDES: http://apprendre-python.com/page-tkinter-interface-graphique-python-tutoriel
    
    #---------------------------------------Importante LIB---------------------------------------
    import os                                                   #Blibliotheque permettant l'interaction avec le systeme
    import sys                                                  #Blibliotheque permettant l'interaction avec le systeme
    import datetime                                             #Blibliotheque permettant d'obtenir la date
    import time                                                 #Blibliotheque permettant d'obtenir la date
    
    import getpass                                              #On importe la blibliotheque "getpass"
    USERNAME = getpass.getuser()                                #On enregistre le Nom de l'Utilisateur
    
    from Tkinter import * #Python Version 2                     #Blibliotheque permettant d'obtenir Tkinter(G.U.I)
    import ttk                                                  #Blibliotheque permettant de charger un composant Tkinter(G.U.I)
    #---------------------------------------Importante LIB---------------------------------------
    
    #-----------------------------------------------------Localisation de l'emplacement des fichiers necessaires-----------------------------------------------------
    print("\n Bonjour/Bonsoir, ne pas faire fonctionner ce programme en utilisant les droits/commandes administrateur si l'utilisateur n'est pas l'Admin au quel cas le programme ne fonctionnera pas correctement. \n") #Information a lire dans la console
    sys.path.append('/home/'+USERNAME+'/CrytpoView_Projet/Services')              #On indique au systeme ou ce situe le repertoire "Services" dans l'Appareil
    #print(USERNAME)                                                              #Test debug
    
    from nettoyage_du_cache import clear_cache                  #Bibliotheque permettant de nettoyer les fichiers cache PYTHON
    
    from Infos_Hardware import CPU_usage                        #Obtention de l'utilisation du Processeur par le Systeme d'exploitation et ses programmes autour
    from Infos_Hardware import CPU_temp                         #Obtention de la Temperature du Processeur sur la carte mere
    from Infos_Hardware import SoC_info                         #Obtention des informations concernant le package CPU+GPU
    from Infos_Hardware import MEM_info                         #Obtention de l'utilisation de la Memoire Vive du Systeme
    #-----------------------------------------------------Localisation de l'emplacement des fichiers necessaires-----------------------------------------------------
    
    #-------------Fenetre Maitre-------------
    fenetre = Tk()              #Creation d'une Fenetre Maîtresse TK appeler "fenetre"
    #-------------Fenetre Maitre-------------
    
    #-------------------------------------------------------------------Contenue Fenetre Principale-------------------------------------------------------------------
    #------------------------------------------------------------------------------     #Affichage du Temps HEURES/MINUTES/SECONDES
    def temps_actuel():   
        #OBTENTION DE L'HEURE ACTUEL sous format HEURE,MINUTE,SECONDE
        #-- DEBUT -- Heure,Minute,Seconde
        tt = time.time()
        system_time = datetime.datetime.fromtimestamp(tt).strftime('%H:%M:%S')
        print ("Voici l'heure:",system_time)
        return system_time
        #-- FIN -- Heure,Minute,Seconde
    #---------------------------------------------
    status_temps_actuel = Label(fenetre, text=temps_actuel())                   #Affichage du Temps (Label)
    status_temps_actuel.pack()                                                  #Pour obtenir un affichage dynamique , Il faut utiliser pack/grid de cette façon
    #---------------------------------------------
    def update_temps_actuel():                                                  #Fonctionnalité permettant de mettre à jour l'Heure en fonction du Temps Réel
        # On met à jour le temps actuel dans le champs text du Widget LABEL pour afficher l'heure
        status_temps_actuel["text"] = temps_actuel()
    
        # Après une seconde , on met à jour le contenue text du LABEL
        fenetre.after(1000, update_temps_actuel)    
    #------------------------------------------------------------------------------
    
    #------------------------------------------------------------------------------
    def information_Materiel():
        #Obtention des Informations Materiel de l'Ordinateur
        global tk_UtilisationCPU
        global tk_tk_cputemp
        global tk_MemoireUtilise
    
        #--        
        UtilisationCPU = CPU_usage()                                                #Obtention du Niveau d'utilisation du Processeur.
        MemoireUtilise = MEM_info()                                                 #Obtention d'information par rapport à la Memoire Vive.
        tk_cputemp = CPU_temp()                                                     #Obtention de la Temperature du Package Processeur/GPU.
        mesure_voltage,memoire_processeur,memoire_gpu  = SoC_info()                 #Obtention d'information par rapport au Couple CPU/GPU.
        
        #--
    
        #--Affichage--
        EnveloppeInfoMateriel = LabelFrame(fenetre, text="Informations Relatives aux Matériels", padx=5, pady=5)    #Création d'une "Zone Frame" à Label
        EnveloppeInfoMateriel.pack(fill="both", expand="no")                                                        #Position de la "Zone Frame" à Label dans la fenêtre
    
        tk_UtilisationCPU = Label(EnveloppeInfoMateriel, text=UtilisationCPU)
        tk_MemoireUtilise = Label(EnveloppeInfoMateriel, text=MemoireUtilise)
        tk_tk_cputemp = Label(EnveloppeInfoMateriel, text=tk_cputemp)
        
        tk_UtilisationCPU.pack()
        tk_MemoireUtilise.pack()
        tk_tk_cputemp.pack()    
        #--Affichage--
    
    def update_information_Materiel():
        #Mise a Jour des Informations a Propos du Materiel
        tk_UtilisationCPU["text"] = CPU_usage()
        tk_MemoireUtilise["text"] = MEM_info()
        tk_tk_cputemp["text"] = CPU_temp()    
    
        # Après une seconde , on met à jour le contenue text du LABEL
        fenetre.after(1000, update_information_Materiel)
    #---
    information_Materiel() #Lancement de la Fonctionnalitée.
    #------------------------------------------------------------------------------
    #------------------------------------------------------------------------------
    def information_Complementaire():
        #Recuperation des Informations
    
        INFOS = "Aucune Informations Supp. à affichée pour le moment."
        
        #--Affichage--
        EnveloppeInfoComplementaire = LabelFrame(fenetre, text="Informations Complémentaires", padx=5, pady=5)    #Création d'une "Zone Frame" à Label
        EnveloppeInfoComplementaire.pack(fill="both", expand="no")
    
    
        #---Affichage Numero d'Urgence---
        tk_info_supp = Label(EnveloppeInfoComplementaire, text=INFOS)
        tk_info_supp.pack()
        #---Affichage Numero d'Urgence---
    
        
        #--Affichage--
    
    #def update_information_Complementaire():
    #    #Mise à Jour des Informations reçues
    #    tk_tk_tel_urgence["text"] = numero_urgence()
    #
    #    # Après X seconde , on met à jour le contenue text du LABEL
    #    fenetre.after(500013, update_information_Complementaire)
    #---
    information_Complementaire() #Lancement de la Fonctionnalitée.
    #------------------------------------------------------------------------------
    
    #-------------------------------------------------------------------Contenue Fenetre Principale-------------------------------------------------------------------
    
    
    
    if __name__ == "__main__":
        try:
            clear_cache()
    
            #-------------------------------------------------------------------Demarrage des fonctions operant sur la Fenetre Principale-------------------------------------------------------------------
            #Récupération des informations pour la Mise à jour du LABEL toute les 1 milliseconde quand la fenêtre Maitre est lancée
            fenetre.after(1, update_temps_actuel)               #update_temps_actuel()
            fenetre.after(1, update_information_Materiel)       #update_information_Materiel()
            #fenetre.after(1, update_information_Complementaire) #update_information_Complementaire()
            #-------------------------------------------------------------------Demarrage des fonctions operant sur la Fenetre Principale-------------------------------------------------------------------
    
    
            fenetre.mainloop()                                  #Boucle de Lancement de la Fenêtre PRINCIPAL
            pass
    
                                                                             #---!!!GESTION DES ERREURS!!!---
    
        except TypeError:
    	#print("Le signal GPS est degradé , veuillez-vous deplacez!")                   #On affiche ce message dans la console                              
    	print("Code Erreur: TypeError")
    	clear_cache()
        except KeyError:
    	#print("API Geocoder a planté, il faut recommencer une nouvelle fois ;=)")      #On affiche ce message dans la console                              
    	print("Code Erreur: KeyError")
            clear_cache()      
        except ValueError:
    	#print("Le signal GPS est degradé , veuillez-vous deplacez!")                   #On affiche ce message dans la console
            print("Code Erreur: ValueError")
            clear_cache()
        except AssertionError:
    	#print("Le Signal GPS est degradé , veuillez-vous deplacez!")                   #On affiche ce message dans la console
            print("Code Erreur: AssertionError")
            clear_cache()
        except NameError:
    	print("Il est necessaire de Redemarrez le Programme!")                          #On affiche ce message dans la console
            print("Code Erreur: NameError")
            clear_cache()
        except:
    	print("Il est necessaire de Redemarrez le Logiciel!")                           #On affiche ce message dans la console
            print("Code Erreur: Aucun")
            clear_cache()
                                                                             #---!!!GESTION DES ERREURS!!!---
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
