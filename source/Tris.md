---
title: Tris
date: 2020-05-07
---
Example Python program Tris.py

## Modules

* import tkinter
* import pygame
* from pandas import *
* from tkinter import *
* from tkinter import messagebox

## Methods

* def ControllaVittoria():

## Code

Python tkinter example

    import tkinter
    
    import pygame
    from pandas import *
    from tkinter import *
    from tkinter import messagebox
    
    def ControllaVittoria():
           # Vedo se ha vinto in verticale
        if posizione_delle_x[0][0] == posizione_delle_x[1][0] == posizione_delle_x[2][0]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
        elif posizione_delle_x[0][1] == posizione_delle_x[1][1] == posizione_delle_x[2][1]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
        elif posizione_delle_x[0][2] == posizione_delle_x[1][2] == posizione_delle_x[2][2]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
    
            # Vedo se ha vinto nella linea orizzontale
        if posizione_delle_x[0][0] == posizione_delle_x[0][1] == posizione_delle_x[0][2]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
        elif posizione_delle_x[1][0] == posizione_delle_x[1][1] == posizione_delle_x[1][2]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
        elif posizione_delle_x[2][0] == posizione_delle_x[2][1] == posizione_delle_x[2][2]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
    
            # Vedo se ha vinto in 1 diagonale
        if posizione_delle_x[0][0] == posizione_delle_x[1][1] == posizione_delle_x[2][2]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
    
            # Vedo se ha vinto nell'altra diagonale
        if posizione_delle_x[0][2] == posizione_delle_x[1][1] == posizione_delle_x[2][0]:
            root = tkinter.Tk()
            root.withdraw()
            messagebox.showinfo('Vittoria', 'Il giocatore %s ha vinto premi spazio per resettare' % giocatore)
    
    pygame.init()
    
    win = pygame.display.set_mode((550,550))
    
    pygame.display.set_caption("Tris")
    
    #Stampo i rettangoli e li aggiungo alle liste
    x = 25
    y = 25
    
    #Ho inizializzato alla matrice valori sopra il 3 cosi non interferiscono con il punteggio della partita
    posizione_delle_x = [[0 for x in range(3)] for y in range(3)]
    a = 5
    for l in range(3):
        for p in range(3):
            posizione_delle_x[l][p] = a
            a += 5
    
    
    lista = []
    lista2 = []
    for i in range(1,10):
        rett = pygame.draw.rect(win, (255, 255, 255), (x, y, 150, 150))
        lista.append(((255, 255, 255), [x, y, 150, 150]))
        lista2.append(rett)
        x+=175
        if i % 3 == 0:
            y += 175
            x = 25
    funzione = True
    cont = 0
    cont_board = 0
    while funzione:
    
        for evento in pygame.event.get():
            if evento.type == pygame.QUIT:
                funzione = False
            #Se spazio è premuto allora cancello tutto
            if evento.type == pygame.KEYDOWN:
                if evento.key == pygame.K_SPACE:
                    a = 5
                    l = 0
                    p = 0
                    for l in range(3):
                        for p in range(3):
                            posizione_delle_x[l][p] = a
                            a += 5
                    lista = []
                    lista2 = []
                    x = 25
                    y = 25
                    cont = 0
                    # Riscrivo tutto perchè è stato premuto spazio
                    for i in range(1, 10):
                        rett = pygame.draw.rect(win, (255, 255, 255), (x, y, 150, 150))
                        lista.append(((255, 255, 255), [x, y, 150, 150]))
                        lista2.append(rett)
                        x += 175
                        if i % 3 == 0:
                            y += 175
                            x = 25
    
            #Vedo la posizone del click del mouse
            if evento.type == pygame.MOUSEBUTTONUP:
                posizione = pygame.mouse.get_pos()
                for i in range(0,9):
                    #Se il click è dentro un quadrato allora lo coloro
                     if lista2[i].collidepoint(posizione):
                        #Se le volte premute dal player è pari e su quella casella non c'è goà un colore allora mette il colore rosso
                        if cont % 2 == 0 and lista[i] != True:
                            giocatore = "Rosso"
                            color, (x, y, w, h) = lista[i]
                            color=(255,0,0)
                            lista[i] = True
                            cont_board = i
                            #visto che la matrice è composta da 3x3 ovviamente non si può superare il valore 2
                            #quindi sottraggo -6 o -3 cosi da avere posizione 0,1 o 2
                            if i >= 6:
                                cont_board = cont_board - 6
                            elif i >= 3:
                                cont_board = cont_board - 3
                            # in base a i che indica la posizone dei quadrati per esempio i = 0
                            # è il prima quadrato cioè quello in alto a sinistra i = 1 è quello affianco ecc
                            if i < 3:
                                posizione_delle_x[0][cont_board] = 1
                            elif i < 6:
                                posizione_delle_x[1][cont_board] = 1
                            else:
                                posizione_delle_x[2][cont_board] = 1
                            ControllaVittoria()
                            cont += 1
                            cont_board += 1
                        #Se le volte premute dal player è pari e su quella casella non c'è goà un colore allora mette il colore blu
                        elif cont % 2 != 0 and lista[i] != True:
                            giocatore = "Blu"
                            color, (x, y, w, h) = lista[i]
                            color=(0,0,255)
                            lista[i] = True
                            cont_board = i
                            if i >= 6:
                                cont_board = cont_board - 6
                            elif i >= 3:
                                cont_board = cont_board - 3
                            #in base a i che indica la posizone dei quadrati per esempio i = 0
                            #è il prima quadrato cioè quello in alto a sinistra i = 1 è quello affianco ecc
                            if i < 3:
                                posizione_delle_x[0][cont_board] = 2
                            elif i < 6:
                                posizione_delle_x[1][cont_board] = 2
                            else:
                                posizione_delle_x[2][cont_board] = 2
                            ControllaVittoria()
    
                            cont_board += 1
                            cont += 1
                        pygame.draw.rect(win, color, pygame.Rect(x, y, w, h))
                        #Se il contatore raggiunge 9 e nessuno dei 2 giocatori ha vinto allora è un pareggio
                        if cont == 9:
                            root = tkinter.Tk()
                            root.withdraw()
                            messagebox.showinfo('Pareggio', 'Nessuno dei 2 giocatori ha vinto')
        pygame.display.update()
    pygame.quit()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
