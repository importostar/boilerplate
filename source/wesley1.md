---
title: wesley1
date: 2020-05-07
---
Example Python program wesley1.py

## Modules

* from tkinter import messagebox
* from tkinter import *

## Methods

* def resultado():

## Code

Python tkinter example

    from tkinter import messagebox
    from tkinter import *
    janela = tkinter.Tk()
    janela.title('MEDIA ALUNO')
    janela.configure(background='#000000')
    rotulo = tkinter.Label(janela, text='»»»»»DESCUBRA SE VOCE FOI APROVADO OU REPROVADO NA ESCOLA«««««««',bg='#FFB6C1')
    rotulo.pack()
    rotulo2 = LabelFrame(janela, text="-AVISO!!!!!!!!",bg='#FFB6C1')
    rotulo2.pack(fill="both", expand="yes")
    
    rotulo3 = Label(rotulo2, text="-ANTES DE COMEÇAR,LEMBRRE-SE QUE NAO E PERMITIDO O USO DE (VIRGULAS),APENAS (PONTOS)",bg='#FFB6C1')
    rotulo3.pack()
    
    rotulonome =tkinter.Label(janela,text='DIGITE O PRIMEIRO NOME DO ALUNO: ',bg='#FFB6C1')  # input»comando tipo pergunta ex:digite alguma coisa
    rotulonome.pack()
    camponome = tkinter.Entry(bd =5)
    camponome.pack()
    rotulom1 = tkinter.Label(janela,text='DIGITE A MEDIA DA ESCOLA DO ALUNO: ',bg='#FFB6C1')
    rotulom1.pack()
    campom1 = tkinter.Spinbox(from_=0, to=10)
    campom1.pack()
    rotulon1 = tkinter.Label(janela,text='DIGITE A PRIMEIRA NOTA: ',bg='#FFB6C1',bd =5)  # nao precisa informar o tipo da variavel,da o nome e qqr valor
    rotulon1.pack()
    campon1 = tkinter.Entry()
    campon1.pack()
    rotulon2 = tkinter.Label(janela,text='DIGITE A SEGUNDA NOTA: ',bg='#FFB6C1')  # mais precisa declarar a variavel sempre
    rotulon2.pack()
    campon2 = tkinter.Entry(bd =5)
    campon2.pack()
    rotulon3 = tkinter.Label(janela,text='DIGITE A TERCEIRA NOTA: ',bg='#FFB6C1')
    rotulon3.pack()
    campon3 = tkinter.Entry(bd =5)
    campon3.pack()
    rotulon4 = tkinter.Label(janela,text='DIGITE A QUARTA NOTA: ',bg='#FFB6C1')  # variaveis:int==inteiro:str==string e float
    rotulon4.pack()
    campon4 = tkinter.Entry(bd =5)
    campon4.pack()
    
    
    def resultado():
     soma1 = float(campon1.get())+float(campon2.get())+float(campon3.get())+float(campon4.get())
     soma = soma1 / 4
     if soma <= float(campom1.get()):
        tkinter.messagebox.showinfo('»RESULTADO«',(camponome.get(),'SE FUDEU!! ALUNO REPROVADO\n A MEDIA DO ALUNO É: ' +str(soma)))
     else:
        tkinter.messagebox.showinfo('»RESULTADO«',(camponome.get(),'ALUNO APROVADO \n a media do aluno e: ' + str(soma)))
    botao = tkinter.Button(janela, text='ENVIAR',bg='#FFB6C1', command=resultado)
    botao.pack()
    
    janela.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
